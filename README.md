# n8n JobFind AI Agent

An AI-powered job search automation workflow built with **n8n**. This workflow intelligently processes job inquiries using the **Groq LLM** and sends real-time notifications via **Telegram**.

## Features

- 🤖 **AI Agent Integration**: Uses Groq's advanced language models for intelligent job matching
- 📱 **Telegram Notifications**: Real-time job updates directly to your Telegram
- 🔄 **Webhook Automation**: Automated workflow triggering via webhooks
- 📝 **Smart Processing**: AI-powered analysis and matching of job requirements
- 🔐 **Secure Configuration**: Environment-based API key management

## Prerequisites

Before you begin, you'll need:

- [n8n](https://n8n.io) (self-hosted or cloud)
- [Groq API Key](https://console.groq.com) (Free tier available)
- [Telegram Bot Token](https://core.telegram.org/bots#botfather)
- A Telegram account

## Installation

### 1. Import the Workflow

1. Download the workflow JSON file from this repository
2. In n8n, click **Import workflow** (or use the menu: Workflows > Import)
3. Select the downloaded JSON file
4. Click **Import**

### 2. Get Groq API Key

#### Step-by-Step Guide:

1. **Visit Groq Console**: https://console.groq.com
2. **Sign up/Login** with your email or Google account
3. **Navigate to API Keys**:
   - Click your profile icon (top right)
   - Select "API Keys"
4. **Create New Key**:
   - Click "Create API Key"
   - Copy the generated key
   - Save it securely (you won't see it again)

#### Groq API Resources:
- **Official Docs**: https://console.groq.com/docs
- **Pricing**: https://console.groq.com/pricing (Free tier: 30 requests/minute)
- **API Reference**: https://console.groq.com/docs/api-reference

**Free Model Options**:
- Llama 2 70B
- Mixtral 8x7B
- Gemma 7B

### 3. Get Telegram Bot Token

#### Step-by-Step Guide:

1. **Open Telegram** (mobile app or web: https://web.telegram.org)
2. **Search for BotFather**:
   - Search for @BotFather
   - Click on "BotFather" (verified bot with blue checkmark)
3. **Create a New Bot**:
   - Send: `/newbot`
   - Choose a name for your bot (e.g., "JobFind AI Bot")
   - Choose a username (must be unique, ends with "bot")
   - BotFather will give you the **API Token**
4. **Copy Your Token**:
   - It looks like: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`
   - Save it securely
5. **Get Your Chat ID**:
   - Start your bot: `/start`
   - Send a message to your bot
   - Visit: https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates
   - Replace `<YOUR_TOKEN>` with your bot token
   - Find your chat ID in the response (look for "chat":{"id":123456789})

#### Telegram Resources:
- **BotFather**: https://t.me/botfather
- **Bot API Docs**: https://core.telegram.org/bots/api
- **Getting Chat ID**: https://core.telegram.org/bots#creating-a-new-bot

## Configuration

### Setting Up API Keys in n8n

1. **Open the Workflow**
2. **Configure Groq Chat Model Node**:
   - Click on "Groq Chat Model" node
   - Click **Credentials** dropdown
   - Click **Create New Credential**
   - Paste your **Groq API Key**
   - Save

3. **Configure Telegram Node**:
   - Click on "Send a text message" node
   - Click **Credentials** dropdown
   - Click **Create New Credential**
   - Paste your **Telegram Bot Token**
   - Save

4. **Update Chat ID**:
   - In the Telegram node, enter your **Chat ID** in the message recipient field

## Workflow Structure

```
Webhook (Trigger)
    ↓
AI Agent (Groq)
    ↓
HTTP Request (Optional data processing)
    ↓
Respond to Webhook
    ↓
Telegram Notification
```

## Usage

### Running the Workflow

1. **Via Webhook**:
   - Copy the webhook URL from the Webhook trigger node
   - Send a POST request with your job query
   - Example: `curl -X POST https://your-n8n-webhook-url -H "Content-Type: application/json" -d '{"query": "Find software engineering jobs"}'`

2. **Via n8n Interface**:
   - Click the "Execute workflow" button
   - View logs in the "Logs" tab

### Testing

1. Enable the workflow (toggle in top right)
2. Click "Execute workflow"
3. You should receive a Telegram notification

## Troubleshooting

### Common Issues

**Issue**: "Invalid API Key" error
- **Solution**: Verify your Groq API key is correct and hasn't expired. Re-generate if needed.

**Issue**: Telegram message not received
- **Solution**: 
  - Check your Bot Token is correct
  - Verify Chat ID is set properly
  - Ensure your bot is started (`/start` in Telegram)
  - Check workflow execution logs

**Issue**: Groq rate limiting
- **Solution**: 
  - Wait a few seconds before next request
  - Upgrade to paid Groq plan for higher limits
  - Current free tier: 30 requests/minute

## API Documentation Links

- **n8n Docs**: https://docs.n8n.io
- **Groq API**: https://console.groq.com/docs/speech-text
- **Telegram Bot API**: https://core.telegram.org/bots/api
- **n8n Groq Integration**: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.groq

## Environment Variables

For production deployments, use environment variables:

```bash
GROQ_API_KEY=your_groq_api_key_here
TELEGRAM_BOT_TOKEN=your_telegram_bot_token_here
TELEGRAM_CHAT_ID=your_chat_id_here
```

## Security

- Never commit API keys to version control
- Use n8n's credential system for secure storage
- Regularly rotate your API keys
- Review webhook access logs

## Support

For issues or questions:
- Check n8n documentation: https://docs.n8n.io
- Visit Groq community: https://console.groq.com/community
- Telegram Bot help: https://core.telegram.org/bots

## Contributing

Contributions are welcome! Feel free to submit issues and pull requests.

Feel free to use and modify

**Created with ♥ for job seekers and automation enthusiasts**
