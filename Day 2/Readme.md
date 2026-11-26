<h1>DAY 2 TASK</h1>
<h2>Prompt parts</h2>
<p>Deleted RULES </p>
<p>Me : Can you deliver in 1 hour? </p>
<p>Bot : Hi! Thanks for reaching out. We love to serve you, but we need a 24‑hour notice for orders. Unfortunately we can’t deliver in one hour. We do offer egg‑free cakes—let me know what you’d like and we’ll schedule it for you! </p>
<p><strong>Added RULES</strong></p>
<p>Me : Can you deliver in 1 hour?</p>
<p>Bot: I’m sorry, we need 24‑hour notice for orders. I’ll check with the owner about an earlier delivery.</p>
<H2>FEW SHOTS</H2>
<P>Built a classifier for my <strong> Sri sai clinic </strong></P>
<p>Classifiers : question , complaint , order</p>
<p><strong>Tested on five messages </strong></p>
<ul>
   <li> Me : "Can you schedule a visit for Rahul on Saturday evening at 6 PM?"</li>
    <li>Bot : Order</li>
    <li>Me : "Do I need to bring my previous blood test reports?"</li>
  <li>Bot : Question </li>
    <li>"Me : The receptionist was very rude when I called earlier today."</li>
  <li>Bot : Complaint</li>
   <li>Me : "Please book a slot for me this Monday morning."</li>
   <li>Bot: Order</li>
    <li>Me : "What time does Dr. Ramesh arrive in the evening?"</li>
  <li>Bot : question</li>
</ul>

<h2>JSON</h2>
<p>Asked the bot to return the order as  JSON With name , item ,qty , date and eggless </p>
<p>Bot : failed to parse JSON: Expecting value: line 1 column 1 (char 0)
Raw response was: Hi! 👋 I’m Sweet Crumbs’ assistant. May I know your name and which egg‑less cake you’d like? (Plum ₹500, Chocolate ₹650, Cupcake ₹80) We need a 24‑hour notice for orders.</p>
<p>As of now it don't have History or database to store the details. so it failed to give the JSON format.</p>
<p>When i set MAX_TURNS = 2 it hold the last 2 conversation. So in our case i asked 3 question after telling my name , so it last 2 question override the name. </p></p>

<h2>MEMORY</h2>
<p>Set MAX_TURNS = 2 and told my name to the bot and asked a few another 3 questions. Later i asked what is my name then Bot replied.</p>
<p>Bot : I’m sorry, but I don’t have that information. If you’d like to book an appointment, please let me know your full name, the date, and the time you’d like to visit.
</p>
<p>MAX_TURNS able to store the messages of the user and bot in message list. when i set MAX_TURNS=2 then it able to hold the last two messages. In above case i told my name and made 3 messages with bot. so it last two message override the previous one.</p>
