# Exno.7-Develop a prompt-based application tailored to their personal needs, fostering creativity and practical problem-solving skills while leveraging the capabilities of large language models.

# Date:09-10-2025
# Register no.212222070019
# Aim: To develop a prompt-based application using ChatGPT - To demonstrate how to create a prompt-based application to organize daily tasks, showing the progression from simple to more advanced prompt designs and their corresponding outputs.

#AI Tools Required: 
ChatGPT

# Explanation: 

---

## **Personal Productivity Assistant — Design and Simulation**

### **1. Core Requirements**

| Category                        | Description                                                                                            |
| ------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Interaction Style**           | Natural language interface for intuitive communication (text-based or voice-enabled).                  |
| **Core Capabilities**           | Task management, scheduling, wellness suggestions, and general question-answering.                     |
| **Adaptability**                | Learns from user inputs over time (e.g., adjusts reminder frequency, tone, or wellness tips).          |
| **Reminders & Notifications**   | Alerts for deadlines, meetings, and personal commitments.                                              |
| **Feedback Loop**               | Captures user responses (e.g., “completed”, “snooze”, “don’t remind me again”) to improve suggestions. |
| **Optional Memory Integration** | Stores user preferences like sleep times, work hours, or preferred exercise routines.                  |

---

### **2. Constructing Prompts for Each Function**

| Feature                     | Example LLM Prompt                                                                              | Expected Behavior                                                                            |
| --------------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Daily Task Manager**      | “Add a new task: Submit report by 5 PM tomorrow.” <br> “Show me my pending tasks for today.”    | LLM parses task, stores it with a deadline, and lists tasks on request.                      |
| **Smart Scheduler**         | “Schedule a meeting with John at 3 PM tomorrow.” <br> “Do I have any free time this afternoon?” | LLM identifies time slots, prevents overlaps, and provides a summary of the schedule.        |
| **Wellness Tips Generator** | “Give me a quick wellness tip for today.” <br> “I prefer mental health tips over fitness.”      | Suggests adaptive tips like mindfulness breaks or hydration reminders, based on preferences. |
| **General Queries**         | “What’s the weather today?” <br> “Summarize this article.”                                      | Handles conversational queries outside productivity tasks, acting as a general assistant.    |
| **Feedback & Adaptation**   | “Don’t remind me about water breaks anymore.” <br> “I’d like more fitness suggestions.”         | Updates stored preferences to modify future suggestions.                                     |

---

### **3. Simulation of Natural Interaction (Command-Line Example)**

**User →** *“Remind me to call mom at 6 PM.”*
**Assistant →** “Got it! I’ll remind you to call mom at 6 PM today.”

**User →** *“Add ‘Finish report’ to my task list for tomorrow.”*
**Assistant →** “Task added: ‘Finish report’ due tomorrow. Would you like me to prioritize it?”

**User →** *“Yes, mark it high priority.”*
**Assistant →** “Noted. ‘Finish report’ is now marked as high priority.”

**User →** *“Any wellness tip for today?”*
**Assistant →** “Take a 5-minute break every hour to stretch your neck and wrists. You’ve been active mostly online today.”

**User →** *“I prefer hydration tips instead.”*
**Assistant →** “Understood! I’ll focus on hydration reminders from now on.”

---

### **4. Feedback and Adaptation Process**

| Step                        | Function                                                                       | Description |
| --------------------------- | ------------------------------------------------------------------------------ | ----------- |
| **1. Collect Inputs**       | Monitor user feedback through direct commands (“I don’t like…”, “More of…”).   |             |
| **2. Update Preferences**   | Store user-specific settings (wellness focus, reminder style, preferred time). |             |
| **3. Modify Behavior**      | Adjust future responses and tips according to saved data.                      |             |
| **4. Evaluate Performance** | Track task completion rates, user satisfaction, and engagement levels.         |             |

---

### **5. (Optional) Memory Integration Example**

| Stored Parameter            | Example Value             | Impact                                  |
| --------------------------- | ------------------------- | --------------------------------------- |
| **Preferred reminder time** | 15 minutes before event   | All alerts adjusted accordingly.        |
| **Wellness focus**          | Hydration and mindfulness | Daily suggestions customized.           |
| **Work hours**              | 9 AM – 5 PM               | Limits reminders during personal hours. |
| **Task preference**         | Prioritize “urgent” tasks | Filters and sorts task summaries.       |

---

### **6. Example LLM Workflow**

1. **Input Parsing** — Recognize task-related, schedule-related, or wellness-related intent.
2. **Action Execution** — Perform corresponding action (e.g., add to task list, schedule event).
3. **Response Generation** — Provide concise and friendly feedback.
4. **Preference Learning** — Update internal state based on corrections or confirmations.

---

### **Final Output Summary**

**Personal Productivity Assistant Features:**

* **Daily Task Manager:**

  * Accepts tasks via natural language (e.g., “Remind me to call mom at 6 PM”).
  * Organizes by priority and deadline.
  * Provides daily summaries and pending items.

* **Smart Scheduler:**

  * Schedules events and reminders using contextual understanding.
  * Detects overlaps and free time slots.

* **Wellness Tips Generator:**

  * Suggests adaptive daily tips (hydration, mental health, breaks).
  * Learns user preferences to personalize suggestions.

* **Learning & Adaptation:**

  * Remembers user corrections and adjusts communication tone and focus areas.
  * Supports incremental updates to behavior and recommendations.





# Result: 
The lab exercise resulted in the creation of a prototype concept for a personal assistant powered by large language models. Students were able to:
 Understand how to tailor LLM prompts to real-life applications.
 Foster creativity by designing features suited to their personal or academic lives.
 Learn prompt engineering techniques for optimal interaction with AI tools.
 Experience the versatility and utility of generative AI in solving everyday problems.
