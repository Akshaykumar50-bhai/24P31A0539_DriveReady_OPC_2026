<h2>Day 5: Knowledge Base (RAG), Agent Memory &amp; Evaluation</h2>

<p>This section summarizes the Day 5 implementation for the <strong>Sri Sai Clinic</strong> AI Receptionist Agent, covering ChromaDB vector storage, semantic search tooling, LangGraph state persistence, hallucination guardrails, and automated testing.</p>

<hr>

<h3>1. Your Knowledge (ChromaDB Vector Store)</h3>
<ul>
  <li><strong>Collection Name:</strong> <code>sri_sai_clinic_faq</code></li>
  <li><strong>Knowledge Size:</strong> 16 clinic facts stored in a dictionary (<code>CLINIC_FAQS</code>) and upserted into ChromaDB with <strong>one fact per chunk</strong>.</li>
  <li><strong>Covered Topics:</strong> Doctor details (Dr. Ramesh), 10-minute slot rules, free 7-day follow-ups, MG Road location &amp; parking, wheelchair accessibility, booking modes, walk-in policy, 4-hour cancellation policy, payment methods (UPI/cards/cash), insurance reimbursement, lab tests/ECG, home blood collection (within 5 km for Rs 100), digital report delivery, ground-floor pharmacy, vaccinations, and medical records.</li>
</ul>

<h3>2. Your Search Tool (<code>search_clinic_faq</code>)</h3>
<ul>
  <li><strong>Tool Function:</strong> <code>search_clinic_faq(query: str) -&gt; str</code></li>
  <li><strong>Retrieval Logic:</strong> Queries the <code>sri_sai_clinic_faq</code> ChromaDB collection and returns the top <code>n_results=3</code> most relevant facts formatted as bullet points.</li>
  <li><strong>Docstring Scope:</strong> Explicitly lists all covered policy and facility categories so the LLM routes general clinic inquiries accurately without guessing.</li>
</ul>

<h3>3. Your Agent &amp; Checkpointer Memory</h3>
<ul>
  <li><strong>Architecture:</strong> Built using LangChain's <code>create_agent</code> powered by Groq (<code>openai/gpt-oss-20b</code>) and integrated with LangGraph's <code>MemorySaver()</code> checkpointer.</li>
  <li><strong>Combined Toolset:</strong> Combines Day 4 tools (<code>get_consultation_fee</code>, <code>check_clinic_hours</code>, <code>book_appointment</code>) with the Day 5 RAG tool (<code>search_clinic_faq</code>).</li>
  <li><strong>Thread Isolation Test:</strong> Verified memory separation across two distinct <code>thread_id</code> sessions:
    <ul>
      <li><code>thread_akshay</code>: Correctly answered UPI payment inquiries using <code>search_clinic_faq</code> and maintained isolated conversation state.</li>
      <li><code>thread_ravi</code>: Confirmed zero cross-thread state leakage when asked for user identity while accurately retrieving the clinic address.</li>
    </ul>
  </li>
</ul>

<h3>4. "Break It" Out-of-Scope Guardrail Testing</h3>
<ul>
  <li><strong>Out-of-Scope Prompts Tested:</strong>
    <ol>
      <li><em>"Do you have an MRI machine or X-ray facility?"</em></li>
      <li><em>"Can I book a dental cleaning with Dr. Ramesh?"</em></li>
    </ol>
  </li>
  <li><strong>Behavior &amp; Rule Enforcement:</strong> The agent did <strong>not</strong> hallucinate or invent services. Guided by strict system <code>RULES</code> (<em>"Answer ONLY using facts returned by your tools... DO NOT make anything up"</em>), it safely declined unsupported claims and offered to check with or forward the request to the reception team.</li>
</ul>

<h3>5. Sign-Off Test Suite &amp; Pass Rate</h3>
<table>
  <thead>
    <tr>
      <th>Test #</th>
      <th>Category</th>
      <th>Query</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>Day 4 Tool (Fees)</td>
      <td>How much for 2 appointments?</td>
      <td><strong>PASS</strong> (Rs 600)</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Day 4 Tool (Hours)</td>
      <td>Are you open on Sunday?</td>
      <td><strong>PASS</strong> (Closed)</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Day 5 RAG</td>
      <td>Can someone collect my blood sample from home?</td>
      <td><strong>PASS</strong> (Within 5 km, Rs 100)</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Day 5 RAG</td>
      <td>Do you support cashless insurance?</td>
      <td><strong>PASS</strong> (Itemized bills only)</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Day 5 RAG</td>
      <td>Is my follow-up visit free?</td>
      <td><strong>PASS</strong> (Within 7 days)</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Day 5 RAG</td>
      <td>Is there a pharmacy nearby?</td>
      <td><strong>PASS</strong> (Ground floor)</td>
    </tr>
    <tr>
      <td>7</td>
      <td>Break It (Out-of-Scope)</td>
      <td>Do you have an MRI machine or X-ray facility?</td>
      <td><strong>PASS</strong> (Escalated to reception)</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Break It (Out-of-Scope)</td>
      <td>Can I book a dental cleaning with Dr. Ramesh?</td>
      <td><strong>PASS</strong> (Escalated to reception)</td>
    </tr>
  </tbody>
</table>

<p><strong>Final Pass Rate:</strong> <code>100.0% (8/8)</code> — Exceeds the 80% target threshold.</p>
