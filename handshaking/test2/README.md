## Opening/Closing Handshakes

### Multicore Results

Run testee:

	oberstet@corei7-ubuntu:~/scm/AutobahnPython/examples/websocket/echo_multicore$ ~/pypy-20131102/bin/pypy -u rver.py --workers 4


Run load probe:

	oberstet@corei7-ubuntu:~/scm/wsperf$ time ./wsperf ws://127.0.0.1:9000 8 500000 1000 2000 > results.json

	real	0m38.953s
	user	1m28.652s
	sys	0m51.076s

Analyze results:

	oberstet@corei7-ubuntu:~/scm/wsperf$ ~/pypy-2.1/bin/pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     37041 ms
	             Total:    500000
	           Success:    500000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13498

	     Min:       1.3 ms
	      SD:      20.9 ms
	     Avg:      25.1 ms
	  Median:      17.6 ms
	  q90   :      43.5 ms
	  q95   :      74.1 ms
	  q99   :     105.7 ms
	  q99.9 :     122.2 ms
	  q99.99:     138.5 ms
	     Max:     141.3 ms

Testee output during load test:

	--------------------------------------------------------------------------------
	Worker Statistics (PID 2271)

	Period No.        : 78
	Period duration   : 5.001 s
	Connected clients : 63

	Period
	  Handshakes      :                16710 #                 3341 #/s
	  Echo'ed msgs    :                    0 #                    0 #/s
	  Echo'ed octets  :                    0 B                    0 B/s
	  Wire octets in  :              3341409 B               668149 B/s
	  Wire octets out :              2736933 B               547278 B/s

	Total
	  Handshakes      :               619492 #
	  Echo'ed msgs    :                    0 #
	  Echo'ed octets  :                    0 B
	  Wire octets in  :            123266371 B
	  Wire octets out :            100966927 B
	--------------------------------------------------------------------------------

	--------------------------------------------------------------------------------
	Worker Statistics (PID 2272)

	Period No.        : 78
	Period duration   : 5.000 s
	Connected clients : 53

	Period
	  Handshakes      :                17026 #                 3405 #/s
	  Echo'ed msgs    :                    0 #                    0 #/s
	  Echo'ed octets  :                    0 B                    0 B/s
	  Wire octets in  :              3406482 B               681250 B/s
	  Wire octets out :              2790234 B               558009 B/s

	Total
	  Handshakes      :               630383 #
	  Echo'ed msgs    :                    0 #
	  Echo'ed octets  :                    0 B
	  Wire octets in  :            125435670 B
	  Wire octets out :            102743790 B
	--------------------------------------------------------------------------------

	--------------------------------------------------------------------------------
	Worker Statistics (PID 2273)

	Period No.        : 78
	Period duration   : 5.001 s
	Connected clients : 40

	Period
	  Handshakes      :                16700 #                 3340 #/s
	  Echo'ed msgs    :                    0 #                    0 #/s
	  Echo'ed octets  :                    0 B                    0 B/s
	  Wire octets in  :              3318325 B               663582 B/s
	  Wire octets out :              2718025 B               543537 B/s

	Total
	  Handshakes      :               626841 #
	  Echo'ed msgs    :                    0 #
	  Echo'ed octets  :                    0 B
	  Wire octets in  :            124733399 B
	  Wire octets out :            102168563 B
	--------------------------------------------------------------------------------

	--------------------------------------------------------------------------------
	Worker Statistics (PID 2270)

	Period No.        : 78
	Period duration   : 5.000 s
	Connected clients : 114

	Period
	  Handshakes      :                16825 #                 3365 #/s
	  Echo'ed msgs    :                    0 #                    0 #/s
	  Echo'ed octets  :                    0 B                    0 B/s
	  Wire octets in  :              3344195 B               668787 B/s
	  Wire octets out :              2739215 B               547801 B/s

	Total
	  Handshakes      :               615578 #
	  Echo'ed msgs    :                    0 #
	  Echo'ed octets  :                    0 B
	  Wire octets in  :            122477336 B
	  Wire octets out :            100320632 B
	--------------------------------------------------------------------------------

### Scaling

#### 1 Core

Start `testee` on 1 core:

	$ cd ~/scm/AutobahnPython/examples/websocket/echo_multicore
	$ pypy server.py --wsuri ws://localhost:9000 --workers 1 --silence

Now run `wsperf` from another shell a couple of times to warmup the testee, and *then* another time to get results (without restarting the `testee`)

	$ cd ~/scm/wsperf
	$ time ./wsperf ws://127.0.0.1:9000 8 500000 1000 2000 > results.json

	real	0m54.220s
	user	1m26.356s
	sys	0m59.724s

Run analyze:

	$ cd ~/scm/wsperf
	$ pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     52292 ms
	             Total:    500000
	           Success:    500000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:      9562

	     Min:      24.6 ms
	      SD:      28.9 ms
	     Avg:     123.8 ms
	  Median:     120.7 ms
	  q90   :     161.7 ms
	  q95   :     173.3 ms
	  q99   :     197.5 ms
	  q99.9 :     221.4 ms
	  q99.99:     231.0 ms
	     Max:     256.6 ms


#### 2 Cores

Start `testee` on 2 cores:

	$ cd ~/scm/AutobahnPython/examples/websocket/echo_multicore
	$ pypy server.py --wsuri ws://localhost:9000 --workers 2 --silence

Now run `wsperf` from another shell a couple of times to warmup the testee, and *then* another time to get results (without restarting the `testee`)

	$ cd ~/scm/wsperf
	$ time ./wsperf ws://127.0.0.1:9000 8 500000 1000 2000 > results.json

	real	0m37.218s
	user	1m27.800s
	sys	0m55.768s

Run analyze:

	$ cd ~/scm/wsperf
	$ pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     35310 ms
	             Total:    500000
	           Success:    500000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     14160

	     Min:       1.1 ms
	      SD:      18.8 ms
	     Avg:      63.1 ms
	  Median:      61.5 ms
	  q90   :      86.3 ms
	  q95   :      95.5 ms
	  q99   :     122.3 ms
	  q99.9 :     141.3 ms
	  q99.99:     145.1 ms
	     Max:     154.0 ms


#### 4 Cores

Start `testee` on 4 cores:

	$ cd ~/scm/AutobahnPython/examples/websocket/echo_multicore
	$ pypy server.py --wsuri ws://localhost:9000 --workers 4 --silence

Now run `wsperf` from another shell a couple of times to warmup the testee, and *then* another time to get results (without restarting the `testee`)

	$ cd ~/scm/wsperf
	$ time ./wsperf ws://127.0.0.1:9000 8 500000 1000 2000 > results.json

	real	0m39.305s
	user	1m28.144s
	sys	0m52.280s

Run analyze:

	$ cd ~/scm/wsperf
	$ pypy analyze.py 

	wsperf results - WebSocket Opening Handshake

	          Duration:     37404 ms
	             Total:    500000
	           Success:    500000
	              Fail:         0
	            Fail %:      0.00
	    Handshakes/sec:     13367

	     Min:       0.3 ms
	      SD:      20.0 ms
	     Avg:      24.7 ms
	  Median:      17.7 ms
	  q90   :      42.3 ms
	  q95   :      72.2 ms
	  q99   :     103.6 ms
	  q99.9 :     122.0 ms
	  q99.99:     130.7 ms
	     Max:     133.2 ms
