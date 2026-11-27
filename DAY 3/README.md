<h1>DAY 3 Tasks</h1>

<h2>Tests</h2>
<p>Added 10 customer question and expected answers in the tests.csv (provided in the Day 3 folders).</p>
<p>After running the tests.csv . I got 22% pass rate.</p>
<p>But bot gave answers has customer understandable way. But i gave the expected answers in a simple words. So that is reason why i got the 22%. Most of the answers are correct.</p>

<h2>Improve</h2>
<p>I made a change in the prompt. In the Format i gave the "reply clearly in a 10 simple words" </p>
<p>After running the code i observed a little increase in the pass rate. Previously it has 22% after it became 33%.</p>

<h2>Switch</h2>
<p>I kept <strong>temperature = 1.0</strong> </p>
<p>After running the program. I have noticed a small change int the pass rate. Intailly pass rate value is 33% after that it slightly dropped to 22%.</p>

<h2>Agent or Not</h2>
<p>For booking appointment : Agent </p>
<p>For calculating Price of appointment : plain code</p>
<p>For Asking doctor timings : One LLM call</p>
