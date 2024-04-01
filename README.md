# LLMs in Action: A Cloud Native Story, running on microshift
# Forked from https://github.com/cncf/llm-in-action

# Using Ollama UBI as internal k8s service
https://github.com/williamcaban/ollama-ubi

## with Ollama UBI pod, pull the required model
### This command will download the mistral model for ollama to use

~~
$ ollama pull mistral
~~


~~~
$ oc get pods -A |egrep "keynote|ollama"
ollama                     ollama-serve-6b77c4df5-rq8k8               1/1     Running                    0               3h6m
test                       keynote-66c595b94b-6z6zn                   1/1     Running                    2               2d12h
$ microshift version
MicroShift Version: 4.14.18
Base OCP Version: 4.14.18
$ oc get nodes
NAME         STATUS   ROLES                         AGE     VERSION
node-nvidia   Ready    control-plane,master,worker   3d17h   v1.27.11
$ oc version
Client Version: 4.14.0-202401111553.p0.g286cfa5.assembly.stream-286cfa5
Kustomize Version: v5.0.1
Kubernetes Version: v1.27.11

$ oc get routes -A
NAMESPACE   NAME           HOST                            ADMITTED   SERVICE      TLS
chat        chat-route     chat.apps.example.com           True       chat-svc     
ollama      ollama-route   ollama.apps.example.com         True       ollama-svc   
test        keynote        keynote-test.apps.example.com   True       keynote      

$ oc get pods
NAME                           READY   STATUS    RESTARTS   AGE
ollama-serve-6b77c4df5-rq8k8   1/1     Running   0          3h9m
$ oc rsh ollama-serve-6b77c4df5-rq8k8 
sh-5.1$ ollama list
NAME              	ID          	SIZE  	MODIFIED   
falcon:7b-instruct	4280f7257e73	4.2 GB	2 days ago	
llava:latest      	8dd30f6b0cb1	4.7 GB	2 days ago	
mistral:latest    	61e88e884507	4.1 GB	2 days ago	
sh-5.1$ 
~~~

# Chat front end 
https://github.com/arthur-r-oliveira/chat_application_k8s
