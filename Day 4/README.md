<h1>Day 4  TASKS</h1>
<h2>TOOLS</h2>
<p>I created three tools for my business.</p>
<p><Strong>book_appointment</Strong> : This is used to book the appointments for users.</p>
<p><Strong>get_consultation_fee</Strong> : This is used to get the consultation fee for booking appointment.</p>
<p><Strong>Check_clinic_hours</Strong> : This is used to retrive the clinic working hours and days.</p>

<h2>Pydantic class for one record</h2>
<p>I used pydantic class for the Appointment. Where it turns customer messy messages into a structured format.</p>
<p>Raw: hi doctor dis is Suresh, need 2 come tmrw around 6pm for severe toothache n fever
</p>
<p>Parsed: patient_name='Suresh' date='2026-11-28' time='6pm' symptoms='severe toothache and fever' is_urgent=True</p>
<p>Raw: Plz book slot for Mrs. Lakshmi on Monday morning 10:30 for routine BP check
</p>
<p>Parsed: patient_name='Mrs. Lakshmi' date='Monday' time='10:30' symptoms='routine BP check' is_urgent=False
</p>
<p>Raw: hey can u fix an appt? my name is Priya, coming Friday evening
</p>
<p>Parsed: patient_name='Priya' date='Friday evening' time=None symptoms=None is_urgent=False
</p>

<h3>Rename One Tool</h3>
<p>I rename my tool Check_clinic_hours to tool1 then docstring = "does stuff". In my case agent didn't corrected it instead of it hallucinated the answer and repied according based on system prompts.</p>
