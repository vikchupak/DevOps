curl stands for client URL.

Optionls list full doc:
- https://curl.se/docs/optionswhen.html
- https://curl.se/docs/manpage.html

POST multipart/form-data\
https://reqbin.com/req/c-sma2qrvp/curl-post-form-example

![image](https://github.com/user-attachments/assets/1e884918-d67a-47fb-a5d5-d5b4b4e160e7)

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -F file0=@photo.png \
  -F file1=@photo.jpeg
```

POST application/json\
```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -H "Connection: keep-alive" \
  -d '{"title":"foo","body":"bar","userId":1}'
```

How to use ```\``` in bash for formating\
https://stackoverflow.com/questions/3871332/how-to-tell-bash-that-the-line-continues-on-the-next-line
