# mirror-hub
Docker file used to contruct image by render

# How to use

## Deploy in Render
New → Web Service → Public Git Repository → type in "https://github.com/Qian-Kun/mirror-hub" → Connect → Region(select Singapore) → Compute(select Free) → scroll down to botton, click "Deploy web service"
```
"Available at your primary URL: https://xxx.onrender.com" means web service conducted successfully.
```
## Activate web service

```bash
urls="yourURL" # eg: https://xxx.onrender.com
PROXY=${urls##*//}

# awake(200 or 404)
curl -sS -o /dev/null -w 'root_http=%{http_code} time=%{time_total}s\n' "$PROXY/"

# inspect(200 or 401)
curl -sS -o /dev/null -w 'v2_http=%{http_code}\n' "$PROXY/v2/"

#activate
curl -sS -o /dev/null -w 'root=%{http_code} time=%{time_total}s\n' $urls
curl -sS -o /dev/null -w 'v2=%{http_code} time=%{time_total}s\n' $urls/v2/

# test
docker pull "$PROXY/library/hello-world"

# mydata
docker pull $PROXY/nfcore/viralrecon

```
