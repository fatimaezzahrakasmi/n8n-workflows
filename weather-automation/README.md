<img width="1048" height="354" alt="image" src="https://github.com/user-attachments/assets/94cb9257-a499-4086-a554-a6741c18d235" />

# Weather Automation Workflow

This n8n workflow automatically fetches the daily weather for Tangier and sends it as a Telegram message every day at 7:00 AM.

---

## Workflow Overview

The workflow consists of the following steps:

1. **Schedule Trigger**  
   - Node: `Schedule Trigger`  
   - Triggers the workflow every day at (7:00 AM).

2. **Fetch Weather Data**  
   - Node: `OpenWeatherMap`  
   - Retrieves the current weather data for **Tangier** in **English** using the [OpenWeatherMap API](https://openweathermap.org/api).  
   - Requires valid OpenWeatherMap API credentials.

3. **Format Message**  
   - Node: `Edit Fields`  
   - Formats the weather data into a user-friendly message:  
     ```
     🌤️ Good morning! Here's the weather for today:
     🌡️ Temp: [temperature]°C
     💨 Wind: [wind speed] m/s
     ☁️ Condition: [weather description]
     ```

4. **Send Telegram Message**  
   - Node: `Send a text message`  
   - Sends the formatted weather message to a specific Telegram chat using the [Telegram API](https://core.telegram.org/bots/api).  
   - Requires valid Telegram bot credentials and the `chatId` to send messages.

---

## Setup Instructions

1. **n8n Installation**  
   - Make sure you have [n8n](https://n8n.io/) installed and running.

2. **OpenWeatherMap API**  
   - Sign up at [OpenWeatherMap](https://openweathermap.org/) and get your API key.  
   - Add it to n8n under **Credentials > OpenWeatherMap**.

3. **Telegram Bot**  
   - Create a Telegram bot via [BotFather](https://core.telegram.org/bots#6-botfather) and obtain the API token.  
   - Add it to n8n under **Credentials > Telegram API**.  
   - Use the chat ID of the recipient to send messages.

4. **Import Workflow**  
   - Import this workflow JSON into your n8n instance.

5. **Activate Workflow**  
   - Activate the workflow to enable daily weather notifications at 7:00 AM.

---

## Customization

- **Change City**: Edit the `cityName` field in the `OpenWeatherMap` node.  
- **Change Language**: Modify the `language` field in the `OpenWeatherMap` node.  
- **Change Schedule**: Adjust the `triggerAtHour` in the `Schedule Trigger` node.  
- **Message Format**: Customize the `message` field in the `Edit Fields` node.

---

## Example Output

🌤️ Good morning! Here's the weather for today:

 🌡️ Temp: 25°C
 💨 Wind: 3.5 m/s
 ☁️ Condition: scattered clouds

 
---

## License

This workflow is open-source and free to use. Modify it as needed for your personal or professional projects.


