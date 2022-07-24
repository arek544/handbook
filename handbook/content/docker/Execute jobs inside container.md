# Execute jobs inside container

`#docker` `#execute` `#command` `#exec` `#inside` `#spark` `#pyspark`


```bash
docker exec -i -t container-id path-to-script
```

## Example
### Run PySpark
```bash
docker exec -i -t 7e7896d430f6 /usr/local/spark/bin/pyspark  
```

```raw
Welcome to 
    ____              __   
   / __/__  ___ _____/ /__
  _\ \/ _ \/ _ `/ __/ '_/
 /__ / .__/\_,_/_/ /_/\_\  version 2.4.1   
    /_/
    
Using Python version 3.7.3 (default, Mar 27 2019 23:01:00)SparkSession available as 'spark'.
>>> 
```

### Run standalone Spark job

**example.py**
```python
from pyspark import SparkContext

logFile = "file:///home/jovyan/work/trial.txt"
sc = SparkContext("local", "first app")
logData = sc.textFile(logFile).cache()
numKs = logData.filter(lambda s: 'K.' in s).count()
numTs = logData.filter(lambda s: 'trial' in s).count()
print("Lines with K: %i, lines with trial: %i" % (numKs, numTs))
```

```bash
docker exec -i -t 7e7896d430f6 /usr/local/spark/bin/pyspark /example.py
```

… and you should see this in the stdout stream…

```raw
...19/05/16 08:55:31 INFO DAGScheduler: 
Job 1 finished: count at /home/jovyan/work/countKT.py:6, 
took 0.195248 sLines with K: 1135, lines with trial: 108...
```
