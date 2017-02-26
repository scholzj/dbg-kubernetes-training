# Demo 4: Kubernetes API

* Start `kubectl proxy`
* Use `curl` to browse through the APIs
  * `curl http://127.0.0.1:8001/healthz`
  * `curl http://127.0.0.1:8001/api/v1`
  * `curl http://127.0.0.1:8001/apis`
* Use your browser and explore the APIs. Try for example following URLs:
  * [http://127.0.0.1:8001/healthz](http://127.0.0.1:8001/healthz)
  * [http://127.0.0.1:8001/api/v1](https://localhost:8001/api/v1)
  * [http://127.0.0.1:8001/apis](http://127.0.0.1:8001/apis)
