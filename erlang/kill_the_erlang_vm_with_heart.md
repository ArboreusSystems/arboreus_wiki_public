# Kill the Erlang VM when it is running with -heart.

Based on [Stackoverflow page](http://stackoverflow.com/questions/7217892/is-there-a-way-to-kill-the-erlang-vm-when-it-is-running-with-heart) and used on Linux Ubuntu

```console
$ netstat -tulpn
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:8887          0.0.0.0:*               LISTEN      1303/beam.smp   
tcp        0      0 127.0.0.1:2812          0.0.0.0:*               LISTEN      8355/monit      
tcp        0      0 127.0.0.1:35388         0.0.0.0:*               LISTEN      1303/beam.smp   
tcp6       0      0 :::8083                 :::*                    LISTEN      11429/influxd   
tcp6       0      0 :::8086                 :::*                    LISTEN      11429/influxd
$ lsof -p 1303 | grep txt
beam.smp 1303 root  txt    REG  253,1  2598416 1316163 /usr/lib/erlang/erts-7.1/bin/beam.smp
$ cd /usr/lib/erlang/erts-7.1/bin/ && mv beam.smp old_beam.smp && kill -9 1303
$ netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:6627            0.0.0.0:*               LISTEN      993/java        
tcp        0      0 0.0.0.0:9797            0.0.0.0:*               LISTEN      13474/java      
tcp        0      0 0.0.0.0:2181            0.0.0.0:*               LISTEN      1062/java       
tcp        0      0 127.0.0.1:9990          0.0.0.0:*               LISTEN      13474/java
$ mv old_beam.smp beam.smp
```

For the case of using on FreeBSD need to be adjusted commands.