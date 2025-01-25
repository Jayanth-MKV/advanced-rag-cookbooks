## Install Ollama
Follow - [Ollama Install](https://github.com/ollama/ollama?tab=readme-ov-file#macos)



## DNS Problem while installing llama3 

> Sample Error
```
$ ollama run llama3

pulling manifest
Error: Head "https://dd20bb891979d25aebc8bec07b2b3bbc.r2.cloudflarestorage.com/ollama/docker/registry/v2/blobs/sha256/00/00e1317cbf74d901080d7100f57580ba8dd8de57203072dc6f668324ba545f29/data?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=66040c77ac1b787c3af820529859349a%!F(MISSING)20240422%!F(MISSING)auto%!F(MISSING)s3%!F(MISSING)aws4_request&X-Amz-Date=20240422T112253Z&X-Amz-Expires=1200&X-Amz-SignedHeaders=host&X-Amz-Signature=1d8428ac79caf602f44cc7e7e1b8c6c0bb7155b4f3d2241c8988e92225c1e67b": dial tcp: lookup dd20bb891979d25aebc8bec07b2b3bbc.r2.cloudflarestorage.com: no such host
```
Follow this [YT Link](https://www.youtube.com/watch?v=CkDEZQuk0bU)


## Run pgvector
```
docker run -d \
  -e POSTGRES_DB=ai \
  -e POSTGRES_USER=ai \
  -e POSTGRES_PASSWORD=ai \
  -e PGDATA=/var/lib/postgresql/data/pgdata \
  -v pgvolume:/var/lib/postgresql/data \
  -p 5532:5432 \
  --name pgvector \
  phidata/pgvector:16
```


## make changes in 
### `E:\AI\LLM\RAG\Llama3-rag-ollama\aienv\Lib\site-packages\phi\document\reader\website.py`

```
def _extract_main_content(self, soup: BeautifulSoup) -> str:
        """
        Extracts the main content from a BeautifulSoup object.

        :param soup: The BeautifulSoup object to extract the main content from.
        :return: The main content.
        """
        # Try to find main content by specific tags or class names
        for tag in ["article", "div","meta"]:
            print(tag)
            element1 = soup.find_all(tag)
            if element1:
                arr=""
                for element in element1:
                    print(element.get_text(strip=True, separator=" "))
                    arr+=element.get_text(strip=True, separator=" ")
                return arr

        for class_name in ["content", "main-content", "post-content"]:
            element = soup.find(class_=class_name)
            if element:
                return element.get_text(strip=True, separator=" ")

        return ""
```


For more info: [LINK](https://github.com/phidatahq/phidata/tree/main/cookbook/llms/ollama/rag)