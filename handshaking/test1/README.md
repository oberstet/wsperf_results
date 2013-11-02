## Testing

For system setup, please see the instructions [here](https://github.com/oberstet/scratchbox/blob/master/python/twisted/sharedsocket/README.md).

You can get a multicore enabled AutobahnPython WebSocket echo `testee` from [here](https://github.com/tavendo/AutobahnPython/tree/master/examples/websocket/echo_multicore).


### Opening/Closing Handshakes

#### 1 Core

Start `testee` on 1 core:

	~/pypy-2.1/bin/pypy server.py --wsuri ws://localhost:9000 --workers 1 --silence

Now run `wsperf` a couple of times to warmup, and *then* another couple of times to get results (without restarting the `testee`)

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m22.322s
	user	0m28.000s
	sys	0m19.036s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     21564 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      9274

	     Min:      26.5 ms
	      SD:      26.9 ms
	     Avg:     124.5 ms
	  Median:     123.2 ms
	  q90   :     157.6 ms
	  q95   :     169.1 ms
	  q99   :     189.3 ms
	  q99.9 :     209.2 ms
	  q99.99:     234.4 ms
	     Max:     248.9 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ git status
	# On branch master
	nothing to commit (working directory clean)
	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m21.829s
	user	0m27.516s
	sys	0m19.156s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     21070 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      9492

	     Min:      26.0 ms
	      SD:      25.0 ms
	     Avg:     122.3 ms
	  Median:     121.4 ms
	  q90   :     155.7 ms
	  q95   :     163.2 ms
	  q99   :     188.0 ms
	  q99.9 :     212.4 ms
	  q99.99:     225.1 ms
	     Max:     227.5 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m22.154s
	user	0m28.016s
	sys	0m18.856s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     21398 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      9346

	     Min:      30.3 ms
	      SD:      28.3 ms
	     Avg:     128.5 ms
	  Median:     127.2 ms
	  q90   :     165.3 ms
	  q95   :     178.6 ms
	  q99   :     198.2 ms
	  q99.9 :     218.4 ms
	  q99.99:     234.5 ms
	     Max:     235.8 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ 

#### 2 Cores

Start `testee` on 2 cores:

	~/pypy-2.1/bin/pypy server.py --wsuri ws://localhost:9000 --workers 2 --silence

Now run `wsperf` a couple of times to warmup, and *then* another couple of times to get results (without restarting the `testee`)

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m15.858s
	user	0m29.520s
	sys	0m19.252s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     15093 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13251

	     Min:       2.1 ms
	      SD:      25.7 ms
	     Avg:      71.0 ms
	  Median:      67.9 ms
	  q90   :     105.0 ms
	  q95   :     117.4 ms
	  q99   :     140.7 ms
	  q99.9 :     182.9 ms
	  q99.99:     188.3 ms
	     Max:     190.8 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m15.883s
	user	0m29.520s
	sys	0m19.428s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     15118 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13229

	     Min:       2.0 ms
	      SD:      24.8 ms
	     Avg:      70.6 ms
	  Median:      67.7 ms
	  q90   :     102.0 ms
	  q95   :     114.4 ms
	  q99   :     143.4 ms
	  q99.9 :     175.2 ms
	  q99.99:     181.3 ms
	     Max:     183.3 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m15.858s
	user	0m30.280s
	sys	0m18.652s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     15091 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13252

	     Min:       2.5 ms
	      SD:      25.7 ms
	     Avg:      71.6 ms
	  Median:      67.1 ms
	  q90   :     106.7 ms
	  q95   :     119.6 ms
	  q99   :     143.9 ms
	  q99.9 :     173.0 ms
	  q99.99:     178.3 ms
	     Max:     180.7 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ 

#### 4 Cores

Start `testee` on 4 cores:

	~/pypy-2.1/bin/pypy server.py --wsuri ws://localhost:9000 --workers 4 --silence

Now run `wsperf` a couple of times to warmup, and *then* another couple of times to get results (without restarting the `testee`)

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m15.916s
	user	0m32.260s
	sys	0m18.836s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     15138 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13211

	     Min:       1.6 ms
	      SD:      27.3 ms
	     Avg:      33.5 ms
	  Median:      23.0 ms
	  q90   :      82.5 ms
	  q95   :      93.6 ms
	  q99   :     103.9 ms
	  q99.9 :     119.3 ms
	  q99.99:     131.9 ms
	     Max:     133.5 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m15.921s
	user	0m32.068s
	sys	0m19.000s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     15149 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13202

	     Min:       1.5 ms
	      SD:      28.1 ms
	     Avg:      34.2 ms
	  Median:      23.6 ms
	  q90   :      85.5 ms
	  q95   :      95.4 ms
	  q99   :     107.5 ms
	  q99.9 :     126.3 ms
	  q99.99:     133.0 ms
	     Max:     135.1 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 4 200000 1000 2000 > results.json 

	real	0m15.846s
	user	0m31.960s
	sys	0m18.744s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     15074 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13267

	     Min:       1.4 ms
	      SD:      24.9 ms
	     Avg:      32.6 ms
	  Median:      24.9 ms
	  q90   :      76.8 ms
	  q95   :      89.2 ms
	  q99   :     101.0 ms
	  q99.9 :     111.5 ms
	  q99.99:     121.1 ms
	     Max:     127.8 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ 
