

- ## Instantiate from Dict
	- ```python
	  from pydantic import BaseModel, Field
	  
	  class Article(BaseModel):
	      id: int
	      title: str
	      
	      
	  inst = Article(**{"id":1, "title":"Hello World"})
	  ```
- ## Incremental ID fields in Pydantic
	- ```python
	  
	  from pydantic import BaseModel, Field
	  
	  class C(BaseModel):
	      id: int = Field(default_factory=count(1).__next__)
	  ```
-
- ## Serialize to JSON
	- Serializes all child classes/structures too - equivalent to doing `json.dumps()` on an object
	- ```python
	  c.model_dump_json()
	  ```
- ## Load from JSON
	- Use the static `model_validate_json` function to load:
	- ```python
	  c = Article.model_validate_json(jsonstr)
	  ```