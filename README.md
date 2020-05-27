gRPC issue #1445 (Node.js)
===========================

PREREQUISITES
-------------

- `node`: This requires Node 0.12.x or greater.

INSTALL
-------

   ```sh
   $ # Get the repository
   $ export REPO_ROOT=grpc_node # REPO root can be any directory of your choice
   $ git clone https://github.com/Wambou/grpc_node_example.git $REPO_ROOT
   $ cd $REPO_ROOT

   $ npm install
   ```

TRY IT!
-------

We use the static code generation in this example.

 - Run the server

   ```sh
   $ # from this directory
   $ node ./static_codegen/greeter_server.js &
   ```

 - Run the client

   ```sh
   $ # from this directory
   $ node ./static_codegen/greeter_client.js
   ```

CODE GENERATION
---------------
Code in this example is pre-generated using protoc and the Node gRPC protoc plugin, and the generated code can be found in various `*_pb.js` files. The command line sequence for generating those files is as follows (assuming that `protoc` and `grpc_node_plugin` are present, and starting in the directory which contains this README.md file):

```sh
cd protos
npm install -g grpc-tools
grpc_tools_node_protoc --js_out=import_style=commonjs_strict,binary:../static_codegen/ --grpc_out=../static_codegen --plugin=protoc-gen-grpc=`which grpc_tools_node_protoc_plugin` helloworld.proto
```


FIX
---
The fix is to edit `helloworld_grpc_pb.js` and add replace:
```js
var helloworld_pb = require('./helloworld_pb.js');
```
with
```js
var helloworld_pb = require('./helloworld_pb.js').helloworld;
```

But since this is the generated code, it is easier to use `import_style=commonjs` instead.
