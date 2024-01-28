- [[pydantic]] seems to have better JSON serialization support than dataclasses.
- ## Incremental ID fields in dataclasses:
	- https://stackoverflow.com/questions/71195208/creating-a-unique-id-in-a-python-dataclass
	- ```python
	  @dataclass
	  class C:
	      identifier: int = field(default_factory=count().__next__, init=False)
	  ```