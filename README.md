<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSV Server Setup</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 800px;
            margin: auto;
            padding: 20px;
        }
        code {
            background-color: #f4f4f4;
            padding: 5px;
            border-radius: 5px;
        }
        .copy-btn {
            cursor: pointer;
            color: blue;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>CSV Server Setup</h1>
        <p>Before you begin, ensure that you have Docker installed on your machine.</p>

        <h2>Docker Images</h2>
        <p>Pull the required Docker images using the following commands:</p>
        <code>docker pull infracloudio/csvserver:latest</code><br>
        <code>docker pull prom/prometheus:v2.22.0</code><br>
        <p>Verify the images using the command:</p>
        <code>docker images</code>

        <h2>Bash Script: gencsv.sh</h2>
        <p>Create a Bash script named <code>gencsv.sh</code> with the following content:</p>
        <pre><code>#!/bin/bash
RANDOM=$$
for i in `seq 10`
do
    echo $((i++)), $RANDOM &gt;&gt; inputdata
done
        </code></pre>

        <h2>Input Data</h2>
        <p>Generate input data using the script:</p>
        <code>./gencsv.sh</code><br>
        <p>Verify the generated input data:</p>
        <code>cat inputdata</code><br>
        <pre><code>1, 4807
2, 5190
3, 20188
4, 10304
5, 13997
6, 30370
7, 19196
8, 3112
9, 15143
10, 8948</code></pre>

        <h2>Docker Run Command</h2>
        <p>Run the CSV server container using the following command:</p>
        <code>docker run -d --name csvserver -e CSVSERVER_BORDER='Orange' -v ${PWD}/inputdata:/csvserver/inputdata -p 9393:9300 infracloudio/csvserver</code><br>

        <p>Access the CSV server UI at <a href="http://localhost:9393" target="_blank">http://localhost:9393</a> to interact with the CSV server.</p>
    </div>

    <script>
        document.querySelectorAll('.copy-btn').forEach(function(btn) {
            btn.addEventListener('click', function() {
                var text = btn.parentNode.nextElementSibling.innerText.trim();
                navigator.clipboard.writeText(text);
                alert('Copied to clipboard: ' + text);
            });
        });
    </script>
</body>
</html>
