#Dmm_rsocket
**    Librdmacm accomplish interfaces between TCP and UDP protocol, but go through RDMA network internally. The dmm_rsocket become a Protocol stack in DMM by adapting to the DMM based on the librdmacm 1.1.0 version to framework.**

##Based on the DMM framework

###Compile

**CMakeList.txt defines the compilation process, including two compiled items**

The external project rdmacm could download the librdmacm version automatically and patch it with "rsocket.patch". The patch will add a static library of "libdmm_rdmacm.a" to the original compilation process,and modify the related documents if it's necessary.

Dmm_rsocket compiles the adaptation code mainly for "rsocket_adpt.c", links to libdmm_rdmacm.a, and generates the libdmm_rsocket.so protocol stack module finally.
   
Both can only compile by calling "make dmm_rsocket" instead of compiling automatically because both of them have set flag.


###File List

#####CMakeLists.txt
Cmake compiles the control file, Module_config.json & rd_config.json

In these two example configuration files, the type configuration of RD is "nstack-rsocket" means use RSOCKET protocol stack.

#####Rsocket.patch
For the librdmacm patch, the key modification is to find the point where the epoll event is executed, all using the DMM_RSOCKET macro control.

Other changes are to package the hijacked API so that the code can calls libc's API directly to avoid calls to the hijacked functions in the DMM, all using GSAPI macro control

#####Rsocket_rdma.h
Public header file

#####Rsocket_adpt.c & rsocket_adpt
Rsocket adaptation section, including initialization and adaptation functions

#####Rsocket_in.h
Included in rsocket.c

#####Rsocket_rs.c
Embedded into the end of rsocket.c as an "include"

#####Rsocket_sapi.h
List of libc functions which only be used internally.

##About author

```javascript
  var ihubo = {
    nickName  : "yinan",
  }
```
