### Opening/Closing Handshakes

#### 1 Core

Start `testee` on 1 core:

	~/pypy-2.1/bin/pypy server.py --wsuri ws://localhost:9000 --workers 1 --silence

Now run `wsperf` a couple of times to warmup, and *then* another couple of times to get results (without restarting the `testee`)

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m22.888s
	user	0m34.432s
	sys	0m24.508s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     22108 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      9046

	     Min:      24.2 ms
	      SD:      28.1 ms
	     Avg:     129.9 ms
	  Median:     128.4 ms
	  q90   :     166.2 ms
	  q95   :     181.7 ms
	  q99   :     198.4 ms
	  q99.9 :     220.6 ms
	  q99.99:     231.6 ms
	     Max:     238.0 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m23.146s
	user	0m34.516s
	sys	0m25.120s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     22376 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      8938

	     Min:      24.0 ms
	      SD:      28.6 ms
	     Avg:     132.1 ms
	  Median:     129.7 ms
	  q90   :     171.5 ms
	  q95   :     184.2 ms
	  q99   :     204.5 ms
	  q99.9 :     231.7 ms
	  q99.99:     233.5 ms
	     Max:     239.0 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m23.087s
	user	0m34.672s
	sys	0m25.096s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     22288 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      8973

	     Min:      23.7 ms
	      SD:      32.7 ms
	     Avg:     136.7 ms
	  Median:     134.4 ms
	  q90   :     180.8 ms
	  q95   :     191.2 ms
	  q99   :     219.2 ms
	  q99.9 :     243.5 ms
	  q99.99:     246.4 ms
	     Max:     267.3 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ 

#### 2 Cores

Start `testee` on 2 cores:

	~/pypy-2.1/bin/pypy server.py --wsuri ws://localhost:9000 --workers 2 --silence

Now run `wsperf` a couple of times to warmup, and *then* another couple of times to get results (without restarting the `testee`)

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m15.769s
	user	0m34.416s
	sys	0m22.860s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     14998 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13334

	     Min:       2.9 ms
	      SD:      24.0 ms
	     Avg:      77.5 ms
	  Median:      75.2 ms
	  q90   :     109.0 ms
	  q95   :     122.0 ms
	  q99   :     145.8 ms
	  q99.9 :     175.0 ms
	  q99.99:     180.7 ms
	     Max:     184.0 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m15.562s
	user	0m34.472s
	sys	0m23.568s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     14786 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13526

	     Min:       5.6 ms
	      SD:      22.9 ms
	     Avg:      76.4 ms
	  Median:      73.8 ms
	  q90   :     107.3 ms
	  q95   :     118.7 ms
	  q99   :     140.2 ms
	  q99.9 :     165.8 ms
	  q99.99:     169.6 ms
	     Max:     172.0 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m15.654s
	user	0m34.752s
	sys	0m23.436s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     14883 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13438

	     Min:       2.5 ms
	      SD:      23.2 ms
	     Avg:      75.9 ms
	  Median:      74.3 ms
	  q90   :     105.6 ms
	  q95   :     117.6 ms
	  q99   :     140.7 ms
	  q99.9 :     157.5 ms
	  q99.99:     171.9 ms
	     Max:     174.3 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ 


#### 4 Cores

Start `testee` on 4 cores:

	~/pypy-2.1/bin/pypy server.py --wsuri ws://localhost:9000 --workers 4 --silence

Now run `wsperf` a couple of times to warmup, and *then* another couple of times to get results (without restarting the `testee`)

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m14.996s
	user	0m34.776s
	sys	0m20.988s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     14211 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     14073

	     Min:       1.5 ms
	      SD:      25.3 ms
	     Avg:      44.7 ms
	  Median:      44.3 ms
	  q90   :      77.8 ms
	  q95   :      86.1 ms
	  q99   :     104.9 ms
	  q99.9 :     131.9 ms
	  q99.99:     135.5 ms
	     Max:     137.5 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m15.502s
	user	0m35.092s
	sys	0m20.648s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     14718 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13588

	     Min:       0.4 ms
	      SD:      26.2 ms
	     Avg:      43.5 ms
	  Median:      40.1 ms
	  q90   :      77.7 ms
	  q95   :      87.0 ms
	  q99   :     111.6 ms
	  q99.9 :     130.4 ms
	  q99.99:     134.9 ms
	     Max:     137.8 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 200000 1000 2000 > results.json 

	real	0m15.071s
	user	0m34.960s
	sys	0m20.980s
	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     14250 ms
	             Total:    200000
	           Success:    200000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     14035

	     Min:       1.1 ms
	      SD:      26.0 ms
	     Avg:      43.8 ms
	  Median:      40.8 ms
	  q90   :      77.2 ms
	  q95   :      85.5 ms
	  q99   :     115.0 ms
	  q99.9 :     138.4 ms
	  q99.99:     141.0 ms
	     Max:     144.1 ms


	oberstet@corei7-ubuntu:~/scm/wsperf$ 
