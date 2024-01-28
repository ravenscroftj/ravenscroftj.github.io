## Django and [[postgres]]
- https://docs.djangoproject.com/en/4.2/ref/databases/#postgresql-notes
- `pdm add "psycopg[binary]"`


## Django and [[pytest]]
- use if pytest in sys.argv for db config switch

## Custom Admin Commands
	- https://docs.djangoproject.com/en/5.0/howto/custom-management-commands/
	- > add a management/commands directory to the application. Django
	  will register a manage.py command for each Python module in that directory
	  whose name doesn’t begin with an underscore.

## Django Rest Framework

### Adding Custom Views to a ViewSet

- use `@action` annotation to add additional routes as described [here](https://www.django-rest-framework.org/api-guide/viewsets/#marking-extra-actions-for-routing):
- More examples https://djangocentral.com/how-to-use-action-decorator-in-django-rest-framework/#adding-a-custom-post-action

```python
  from django.contrib.auth.models import User
  from rest_framework import status, viewsets
  from rest_framework.decorators import action
  from rest_framework.response import Response
  from myapp.serializers import UserSerializer, PasswordSerializer
  
  class UserViewSet(viewsets.ModelViewSet):
	  """
	  A viewset that provides the standard actions
	  """
	  queryset = User.objects.all()
	  serializer_class = UserSerializer
  
	  @action(detail=True, methods=['post'])
	  def set_password(self, request, pk=None):
		  user = self.get_object()
		  serializer = PasswordSerializer(data=request.data)
		  if serializer.is_valid():
			  user.set_password(serializer.validated_data['password'])
			  user.save()
			  return Response({'status': 'password set'})
		  else:
			  return Response(serializer.errors,
							  status=status.HTTP_400_BAD_REQUEST)
  
	  @action(detail=False)
	  def recent_users(self, request):
		  recent_users = User.objects.all().order_by('-last_login')
  
		  page = self.paginate_queryset(recent_users)
		  if page is not None:
			  serializer = self.get_serializer(page, many=True)
			  return self.get_paginated_response(serializer.data)
  
		  serializer = self.get_serializer(recent_users, many=True)
		  return Response(serializer.data)
		
  
```
		-