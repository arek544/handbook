# Troubleshooting

#docker #error #troubleshooting

### Troubleshooting

Now, some errors you are likely to experience. If you see no errors, skip this section. First, a typical situation after restarting the container:

```
docker: Error response from daemon: Conflict. The container name "/spark" is already in use by container "f8004cfa18468ad63c7ef26a1a61a446e8367ef32ee69de3d8b6073ef251af73". You have to remove (or rename) that container to be able to reuse that name.
```

This can be fixed simply by removing the stopped container: **docker rm [your-container-handle-here]**

Another possible situation

```
 jupyter/pyspark-notebook  create notebook failed permission denied windows
```

In my case, the directory was read only. Upper directory was read only (windows). Modifying these permissions still did not yield result, the error persisted. I later guessed that this could have been caused by the filesystem type (exFAT). So I moved the local directory to another local drive, formatted with NTFS. Note that NTFS is native to Windows and generally better integrated with this operating system. The error disappeared but instead I got something even more obscure:

```
docker: Error response from daemon: Drive sharing seems blocked by a firewall.See 'docker run --help'.
```

Long story short, this disappeared only after I restarted file and printer sharing in Windows. I unchecked and checked again File and Printer Sharing for Microsoft Networks property. Uninstalled and Installed the property. Then the command did run properly and the Juyter notebook started properly inside the container. Here is one other docker run error that I happen to see once in a while:

```
 C:\sparkMounted>docker run -d -p 8888:8888 (...)docker: Error response from daemon: driver failed programming external connectivity on endpoint spark (...): Error starting userland proxy: mkdir /port/tcp:0.0.0.0:8888:tcp:172.17.0.2:8888: input/output error.
```

This happens after Windows shutdown. The solution: Docker needs to be restarted.