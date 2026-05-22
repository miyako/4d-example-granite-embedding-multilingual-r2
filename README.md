# 4d-example-granite-embedding-multilingual-r2
Granite Embedding Multilingual R2 in GGUF

|`max_position_embeddings`|`hidden_size`|`num_hidden_layers`|`pooling`
|-:|-:|-:|-:|
|`32768`|`768`|`22`|`cls`

```4d
var $llama : cs.AIKit.OpenAI
$llama:=cs.AIKit.OpenAI.new()
$llama.baseURL:="http://127.0.0.1:8082/v1"

var $batch : cs.AIKit.OpenAIEmbeddingsResult
$batch:=$llama.embeddings.create($input)

var $embedding : 4D.Vector
var $inputs : Collection
$inputs:=[]
$inputs.push("Die aktuellen Arbeitslosenzahlen zeigen einen deutlichen Rückgang.")
$inputs.push("The actual unemployment figures were far lower than what the report claimed.")
$inputs.push("Sie zog den Fingerhut über den Zeigefinger, bevor sie mit dem Nähen begann.")
$inputs.push("She pressed the thimble firmly onto her fingertip to push the needle through the thick fabric.")

$batch:=$llama.embeddings.create($inputs)

var $embeddings : Collection
If ($batch.success)
	$embeddings:=$batch.embeddings
	var $cosineSimilarity : Real
	$cosineSimilarity1:=$embeddings[0].embedding.cosineSimilarity($embeddings[1].embedding)
	$cosineSimilarity2:=$embeddings[2].embedding.cosineSimilarity($embeddings[3].embedding)
	ALERT("should score low:"+String($cosineSimilarity1)+"\r"\
	+"should score high:"+String($cosineSimilarity2))
End if 
```

<img width="480" height="175" alt="Screenshot 2026-05-22 at 11 08 30" src="https://github.com/user-attachments/assets/76ceaf19-9039-4245-a11e-07bc1393794e" />
