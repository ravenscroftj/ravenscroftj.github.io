---
date: 2024-03-04
public: true
---

Model serving framework optimised for GPU and CPU environments.

## Editing pbtxt

PBTXT is the protobuf text format. There is a vscode extension that can be used to provide syntax highlighting:

```
Name: Protobuf Text Format
Id: thesofakillers.vscode-pbtxt
Description: Protocol Buffer Text Format syntax highlighting for VS Code
Version: 0.0.4
Publisher: thesofakillers
VS Marketplace Link: https://marketplace.visualstudio.com/items?itemName=thesofakillers.vscode-pbtxt
```

## Triton Ensemble

In Triton an Ensemble doesn’t mean the same as an Ensemble Model. It is more akin to a classification pipeline

### Building an Ensemble

- https://blog.ml6.eu/triton-ensemble-model-for-deploying-transformers-into-production-c0f727c012e3
- We need to install transformers into the docker image
- Added a lightweight docker image:
- 
```dockerfile
FROM nvcr.io/nvidia/tritonserver:24.01-py3

RUN pip3 install transformers
```

- `docker build -t custom_triton .`

## Calling a Triton Model with Text

**Reference:** https://stackoverflow.com/questions/72101578/using-string-parameter-for-nvidia-triton

The key seems to be to tell numpy that the data is an `np.object_`:
```python

import numpy as np

input_text = "We are a medical company that specialises in helping with prosthetic legs"
sector_labels = ['Healthcare', 'Software Hardware', 'Professional Services', 'Industry and Manufacturing']

input_array = np.array([input_text], dtype=np.object_)
labels = np.array([sector_labels], dtype=np.object_)

```

Then we pass the type of `Bytes` to th `InferInput` object for the dtype:

```python
input = httpclient.InferInput("TEXT", input_array.shape, 'BYTES')
input.set_data_from_numpy(input_array)

lbl = httpclient.InferInput("LABELS", labels.shape, 'BYTES')
lbl.set_data_from_numpy(labels)

r = client.infer("ensemble_model", inputs=[input, lbl])
```

## Making Requests to Other Models Within Triton

We can batch up data and make requests to other models:

```python
requests = []
for i in range(0, len(query_inputs), 4):
    batch_inputs = query_inputs[i:i+4]
    batch_labels = labels[i:i+4]

    # Tokenize the batch
    tokens: Dict[str, np.ndarray] = self.tokenizer(
            batch_inputs, batch_labels, return_tensors=TensorType.NUMPY, padding=True
    )   

    
    inputs = []
    for input_name in self.tokenizer.model_input_names:
        tensor_input = pb_utils.Tensor(input_name, tokens[input_name])
        inputs.append(tensor_input)

    inference_request = pb_utils.InferenceRequest(model_name='deberta', correlation_id=i, inputs=inputs, requested_output_names=['logits']).async_exec()
    requests.append( inference_request )

inf_responses = await asyncio.gather(*requests)
```


### `pb_utils` and `InferenceResponse` objects

#### Getting Data out of Response:
- https://github.com/triton-inference-server/server/issues/5952
```python
  for response in inf_responses:
      if response.has_error():
          e = response.error()
          print("Error", e.code(), e.message(), flush=True)
          raise Exception(e.message())
          
      print("Response", response, dir(response), flush=True)

      print("output dir", dir(response.output_tensors()))

      tensor_cpu = pb_utils.get_output_tensor_by_name(response, 'logits')
  
      outputs.append(tensor_cpu.as_numpy())
```


