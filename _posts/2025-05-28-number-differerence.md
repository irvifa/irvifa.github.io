---
layout: post
title: Number Difference
categories: Leetcode
---

# 🎮 Number Difference Game 🎮

An interactive programming challenge that visualizes the difference between sums of numbers divisible and not divisible by a given value.

<div id="number-game-container">
    <style>
        #number-game-container * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        #number-game-container {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 50%, #1a1a1a 100%);
            min-height: 100vh;
            padding: 20px;
            color: #f5f5f5;
            border-radius: 20px;
            margin: 20px 0;
        }

        #number-game-container .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        #number-game-container h1 {
            text-align: center;
            font-size: 2.5em;
            margin-bottom: 30px;
            background: linear-gradient(45deg, #ffffff, #cccccc, #888888);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { filter: drop-shadow(0 0 5px rgba(255, 255, 255, 0.3)); }
            to { filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.6)); }
        }

        #number-game-container .game-section {
            background: rgba(255, 255, 255, 0.03);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        #number-game-container .input-group {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            align-items: center;
            flex-wrap: wrap;
        }

        #number-game-container label {
            font-weight: bold;
            font-size: 1.1em;
            color: #e0e0e0;
        }

        #number-game-container input[type="number"] {
            padding: 12px;
            border: 2px solid #555555;
            border-radius: 10px;
            background: #2a2a2a;
            color: #f5f5f5;
            font-size: 1.1em;
            width: 100px;
            text-align: center;
            transition: all 0.3s ease;
        }

        #number-game-container input[type="number"]:focus {
            outline: none;
            border-color: #888888;
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
            transform: scale(1.05);
            background: #333333;
        }

        #number-game-container .btn {
            padding: 12px 25px;
            border: 2px solid #666666;
            border-radius: 10px;
            background: linear-gradient(45deg, #444444, #666666);
            color: #f5f5f5;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        #number-game-container .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
            background: linear-gradient(45deg, #555555, #777777);
            border-color: #888888;
        }

        #number-game-container .result {
            font-size: 1.5em;
            font-weight: bold;
            text-align: center;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            transition: all 0.5s ease;
            border: 2px solid;
        }

        #number-game-container .result.positive {
            background: linear-gradient(45deg, #333333, #555555);
            border-color: #888888;
            color: #ffffff;
            animation: pulse 1s ease-in-out;
        }

        #number-game-container .result.negative {
            background: linear-gradient(45deg, #1a1a1a, #2d2d2d);
            border-color: #666666;
            color: #cccccc;
            animation: pulse 1s ease-in-out;
        }

        #number-game-container .result.zero {
            background: linear-gradient(45deg, #2a2a2a, #404040);
            border-color: #777777;
            color: #e0e0e0;
            animation: pulse 1s ease-in-out;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        #number-game-container .visualization {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(40px, 1fr));
            gap: 5px;
            margin: 20px 0;
            max-height: 300px;
            overflow-y: auto;
        }

        #number-game-container .number-box {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 8px;
            font-weight: bold;
            font-size: 0.9em;
            transition: all 0.3s ease;
            cursor: pointer;
            border: 2px solid;
        }

        #number-game-container .number-box.divisible {
            background: linear-gradient(45deg, #1a1a1a, #2d2d2d);
            border-color: #555555;
            color: #cccccc;
            animation: bounce 0.6s ease-in-out;
        }

        #number-game-container .number-box.not-divisible {
            background: linear-gradient(45deg, #404040, #555555);
            border-color: #777777;
            color: #ffffff;
            animation: bounce 0.6s ease-in-out;
        }

        @keyframes bounce {
            0%, 20%, 60%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            80% { transform: translateY(-5px); }
        }

        #number-game-container .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        #number-game-container .stat-card {
            background: rgba(255, 255, 255, 0.05);
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }

        #number-game-container .stat-value {
            font-size: 2em;
            font-weight: bold;
            margin-bottom: 5px;
            color: #ffffff;
        }

        #number-game-container .challenge-section {
            background: linear-gradient(45deg, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.02));
            border-radius: 15px;
            padding: 25px;
            margin-top: 30px;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        #number-game-container .challenge-title {
            font-size: 1.5em;
            margin-bottom: 15px;
            text-align: center;
            color: #ffffff;
        }

        #number-game-container .code-editor {
            background: #1a1a1a;
            border-radius: 10px;
            padding: 20px;
            font-family: 'Courier New', monospace;
            color: #e0e0e0;
            font-size: 0.9em;
            overflow-x: auto;
            margin: 15px 0;
            border: 1px solid #333333;
        }

        #number-game-container .language-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        #number-game-container .tab {
            padding: 8px 16px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 8px;
            color: #e0e0e0;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        #number-game-container .tab.active {
            background: linear-gradient(45deg, #444444, #666666);
            border-color: #888888;
            color: #ffffff;
        }

        #number-game-container .tab:hover:not(.active) {
            background: rgba(255, 255, 255, 0.1);
            border-color: rgba(255, 255, 255, 0.3);
        }

        #number-game-container .explanation {
            background: rgba(255, 255, 255, 0.03);
            padding: 20px;
            border-radius: 10px;
            margin: 15px 0;
            border-left: 5px solid #666666;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        #number-game-container h2 {
            color: #ffffff;
            margin-bottom: 15px;
        }

        #number-game-container h3 {
            color: #e0e0e0;
            margin-bottom: 10px;
        }
    </style>

    <div class="container">
        <h1>🎮 Interactive Challenge 🎮</h1>
        
        <div class="game-section">
            <h2>Play the Game</h2>
            <div class="input-group">
                <label for="n">Range (n):</label>
                <input type="number" id="n" value="10" min="1" max="100">
                
                <label for="m">Divisor (m):</label>
                <input type="number" id="m" value="3" min="2" max="20">
                
                <button class="btn" onclick="calculateDifference()">🚀 Calculate!</button>
            </div>
            
            <div id="result" class="result" style="display: none;"></div>
            
            <div class="stats" id="stats" style="display: none;">
                <div class="stat-card">
                    <div class="stat-value" id="totalSum">0</div>
                    <div>Total Sum (1 to n)</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="divisibleSum">0</div>
                    <div>Sum of Divisibles</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="nonDivisibleSum">0</div>
                    <div>Sum of Non-Divisibles</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="finalResult">0</div>
                    <div>Final Difference</div>
                </div>
            </div>
            
            <div id="visualization" class="visualization"></div>
        </div>

        <div class="challenge-section">
            <h2 class="challenge-title">🧑‍💻 Code Implementation</h2>
            
            <div class="language-tabs">
                <button class="tab active" onclick="showCode('cpp')">C++</button>
                <button class="tab" onclick="showCode('python')">Python</button>
                <button class="tab" onclick="showCode('javascript')">JavaScript</button>
                <button class="tab" onclick="showCode('java')">Java</button>
            </div>
            
            <div id="code-cpp" class="code-editor">
<pre><span style="color: #cccccc;">class</span> <span style="color: #ffffff;">Solution</span> {
<span style="color: #cccccc;">public</span>:
    <span style="color: #cccccc;">int</span> <span style="color: #e0e0e0;">differenceOfSums</span>(<span style="color: #cccccc;">int</span> n, <span style="color: #cccccc;">int</span> m) {
        <span style="color: #e0e0e0;">std::vector</span>&lt;<span style="color: #cccccc;">int</span>&gt; numbers(n);
        <span style="color: #e0e0e0;">std::iota</span>(numbers.begin(), numbers.end(), <span style="color: #aaaaaa;">1</span>);
        
        <span style="color: #cccccc;">return</span> <span style="color: #e0e0e0;">std::transform_reduce</span>(numbers.begin(), numbers.end(), <span style="color: #aaaaaa;">0</span>, 
            <span style="color: #e0e0e0;">std::plus</span>&lt;<span style="color: #cccccc;">int</span>&gt;{},
            [m](<span style="color: #cccccc;">int</span> num) { <span style="color: #cccccc;">return</span> num % m == <span style="color: #aaaaaa;">0</span> ? -num : num; });
    }
};</pre>
            </div>
            
            <div id="code-python" class="code-editor" style="display: none;">
<pre><span style="color: #cccccc;">from</span> functools <span style="color: #cccccc;">import</span> reduce
<span style="color: #cccccc;">from</span> operator <span style="color: #cccccc;">import</span> add

<span style="color: #cccccc;">def</span> <span style="color: #e0e0e0;">difference_of_sums</span>(n, m):
    <span style="color: #888888;">"""Calculate difference using functional programming approach"""</span>
    numbers = <span style="color: #e0e0e0;">list</span>(<span style="color: #e0e0e0;">range</span>(<span style="color: #aaaaaa;">1</span>, n + <span style="color: #aaaaaa;">1</span>))
    transformed = <span style="color: #e0e0e0;">map</span>(<span style="color: #cccccc;">lambda</span> num: -num <span style="color: #cccccc;">if</span> num % m == <span style="color: #aaaaaa;">0</span> <span style="color: #cccccc;">else</span> num, numbers)
    
    <span style="color: #cccccc;">return</span> <span style="color: #e0e0e0;">reduce</span>(add, transformed, <span style="color: #aaaaaa;">0</span>)

<span style="color: #888888;"># Alternative using sum() with generator expression:</span>
<span style="color: #cccccc;">def</span> <span style="color: #e0e0e0;">difference_of_sums_modern</span>(n, m):
    <span style="color: #cccccc;">return</span> <span style="color: #e0e0e0;">sum</span>(-num <span style="color: #cccccc;">if</span> num % m == <span style="color: #aaaaaa;">0</span> <span style="color: #cccccc;">else</span> num 
              <span style="color: #cccccc;">for</span> num <span style="color: #cccccc;">in</span> <span style="color: #e0e0e0;">range</span>(<span style="color: #aaaaaa;">1</span>, n + <span style="color: #aaaaaa;">1</span>))</pre>
            </div>
            
            <div id="code-javascript" class="code-editor" style="display: none;">
<pre><span style="color: #cccccc;">function</span> <span style="color: #e0e0e0;">differenceOfSums</span>(n, m) {
    <span style="color: #cccccc;">const</span> numbers = <span style="color: #e0e0e0;">Array</span>.<span style="color: #e0e0e0;">from</span>({length: n}, (_, i) => i + <span style="color: #aaaaaa;">1</span>);
    
    <span style="color: #cccccc;">return</span> numbers
        .<span style="color: #e0e0e0;">map</span>(num => num % m === <span style="color: #aaaaaa;">0</span> ? -num : num)
        .<span style="color: #e0e0e0;">reduce</span>((sum, val) => sum + val, <span style="color: #aaaaaa;">0</span>);
}

<span style="color: #888888;">// Modern ES6+ approach with chaining:</span>
<span style="color: #cccccc;">const</span> <span style="color: #e0e0e0;">differenceOfSums</span> = (n, m) => 
    <span style="color: #e0e0e0;">Array</span>.<span style="color: #e0e0e0;">from</span>({length: n}, (_, i) => i + <span style="color: #aaaaaa;">1</span>)
        .<span style="color: #e0e0e0;">reduce</span>((sum, num) => sum + (num % m === <span style="color: #aaaaaa;">0</span> ? -num : num), <span style="color: #aaaaaa;">0</span>);

<span style="color: #888888;">// Using Array.keys() alternative:</span>
<span style="color: #cccccc;">const</span> <span style="color: #e0e0e0;">differenceOfSumsKeys</span> = (n, m) => 
    [...<span style="color: #e0e0e0;">Array</span>(n).<span style="color: #e0e0e0;">keys</span>()]
        .<span style="color: #e0e0e0;">map</span>(i => i + <span style="color: #aaaaaa;">1</span>)
        .<span style="color: #e0e0e0;">reduce</span>((sum, num) => sum + (num % m === <span style="color: #aaaaaa;">0</span> ? -num : num), <span style="color: #aaaaaa;">0</span>);</pre>
            </div>
            
            <div id="code-java" class="code-editor" style="display: none;">
<pre><span style="color: #cccccc;">import</span> java.util.stream.IntStream;

<span style="color: #cccccc;">public class</span> <span style="color: #ffffff;">Solution</span> {
    <span style="color: #cccccc;">public int</span> <span style="color: #e0e0e0;">differenceOfSums</span>(<span style="color: #cccccc;">int</span> n, <span style="color: #cccccc;">int</span> m) {
        <span style="color: #cccccc;">return</span> <span style="color: #e0e0e0;">IntStream</span>.<span style="color: #e0e0e0;">rangeClosed</span>(<span style="color: #aaaaaa;">1</span>, n)
            .<span style="color: #e0e0e0;">map</span>(num -> num % m == <span style="color: #aaaaaa;">0</span> ? -num : num)
            .<span style="color: #e0e0e0;">sum</span>();
    }
    
    <span style="color: #888888;">// Alternative using reduce for more explicit control:</span>
    <span style="color: #cccccc;">public int</span> <span style="color: #e0e0e0;">differenceOfSumsReduce</span>(<span style="color: #cccccc;">int</span> n, <span style="color: #cccccc;">int</span> m) {
        <span style="color: #cccccc;">return</span> <span style="color: #e0e0e0;">IntStream</span>.<span style="color: #e0e0e0;">rangeClosed</span>(<span style="color: #aaaaaa;">1</span>, n)
            .<span style="color: #e0e0e0;">reduce</span>(<span style="color: #aaaaaa;">0</span>, (sum, num) -> 
                sum + (num % m == <span style="color: #aaaaaa;">0</span> ? -num : num));
    }
    
    <span style="color: #888888;">// Using parallel stream for larger datasets:</span>
    <span style="color: #cccccc;">public int</span> <span style="color: #e0e0e0;">differenceOfSumsParallel</span>(<span style="color: #cccccc;">int</span> n, <span style="color: #cccccc;">int</span> m) {
        <span style="color: #cccccc;">return</span> <span style="color: #e0e0e0;">IntStream</span>.<span style="color: #e0e0e0;">rangeClosed</span>(<span style="color: #aaaaaa;">1</span>, n)
            .<span style="color: #e0e0e0;">parallel</span>()
            .<span style="color: #e0e0e0;">map</span>(num -> num % m == <span style="color: #aaaaaa;">0</span> ? -num : num)
            .<span style="color: #e0e0e0;">sum</span>();
    }
}</pre>
            </div>
            
            <div class="explanation">
                <h3>🎯 How it works:</h3>
                <p><strong>Goal:</strong> Calculate the difference between the sum of numbers NOT divisible by m and the sum of numbers divisible by m.</p>
                <p><strong>Algorithm:</strong> For each number from 1 to n, if it's divisible by m, subtract it from our answer. Otherwise, add it to our answer.</p>
                <p><strong>Math Formula:</strong> result = Σ(non-divisible) - Σ(divisible)</p>
            </div>
        </div>
    </div>
</div>

<script>
    function calculateDifference() {
        const n = parseInt(document.getElementById('n').value);
        const m = parseInt(document.getElementById('m').value);
        
        if (n <= 0 || m <= 0) {
            alert('Please enter positive numbers!');
            return;
        }
        
        if (n > 100) {
            alert('Please keep n ≤ 100 for better visualization!');
            return;
        }
        
        let ans = 0;
        let divisibleSum = 0;
        let nonDivisibleSum = 0;
        let totalSum = 0;
        
        // Clear previous visualization
        const visualization = document.getElementById('visualization');
        visualization.innerHTML = '';
        
        // Calculate and visualize
        for (let i = 1; i <= n; i++) {
            totalSum += i;
            
            const numberBox = document.createElement('div');
            numberBox.className = 'number-box';
            numberBox.textContent = i;
            
            if (i % m === 0) {
                ans -= i;
                divisibleSum += i;
                numberBox.classList.add('divisible');
                numberBox.title = `${i} is divisible by ${m} (subtract)`;
            } else {
                ans += i;
                nonDivisibleSum += i;
                numberBox.classList.add('not-divisible');
                numberBox.title = `${i} is not divisible by ${m} (add)`;
            }
            
            // Add with delay for animation effect
            setTimeout(() => {
                visualization.appendChild(numberBox);
            }, i * 100);
        }
        
        // Show result after animation
        setTimeout(() => {
            const resultDiv = document.getElementById('result');
            resultDiv.textContent = `Result: ${ans}`;
            resultDiv.style.display = 'block';
            
            if (ans > 0) {
                resultDiv.className = 'result positive';
            } else if (ans < 0) {
                resultDiv.className = 'result negative';
            } else {
                resultDiv.className = 'result zero';
            }
            
            // Update stats
            document.getElementById('totalSum').textContent = totalSum;
            document.getElementById('divisibleSum').textContent = divisibleSum;
            document.getElementById('nonDivisibleSum').textContent = nonDivisibleSum;
            document.getElementById('finalResult').textContent = ans;
            document.getElementById('stats').style.display = 'grid';
        }, (n + 1) * 100);
    }
    
    function showCode(language) {
        // Hide all code blocks
        const codeBlocks = document.querySelectorAll('[id^="code-"]');
        codeBlocks.forEach(block => block.style.display = 'none');
        
        // Show selected code block
        document.getElementById(`code-${language}`).style.display = 'block';
        
        // Update tab styles
        const tabs = document.querySelectorAll('.tab');
        tabs.forEach(tab => tab.classList.remove('active'));
        event.target.classList.add('active');
    }
    
    // Initialize with default calculation when page loads
    document.addEventListener('DOMContentLoaded', function() {
        calculateDifference();
    });
</script>