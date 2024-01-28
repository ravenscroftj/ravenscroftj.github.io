## Accurate progress in pool/imap cases
```python
  from multiprocessing import Pool
  from functools import partial
  from tqdm import tqdm
  
  def _generate_company_details(item, data_dir):
      # Your function implementation
      pass
  
  # Assuming you have defined 'threads' and 'iterator' appropriately
  pool = Pool(threads)
  
  # Initialize tqdm progress bar with the total number of items
  pbar = tqdm(total=len(iterator))
  
  # Use pool.imap to process items in parallel
  for item in pool.imap(partial(_generate_company_details, data_dir=data_dir), iterator):
      yield item
      pbar.update(1)  # Update the progress bar after each item is processed
  
  pbar.close()  # Close the progress bar after the loop
  ```