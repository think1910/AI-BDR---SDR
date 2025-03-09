# AIBDR - AI Business Data Researcher Platform

A comprehensive platform for managing, enriching, and leveraging contact data with AI-powered research capabilities.

## Overview

AIBDR combines a modern React-based front-end UI with powerful AI research capabilities to help businesses maintain high-quality contact data. The platform consists of three main components:

1. **UI Front-End**: A React-based web application for managing contacts, folders, campaigns, and templates
2. **Researcher Agent**: A Python-based AI research tool that automatically enriches contact data by searching the web
3. **Personalizor Agent**: A Python-based AI tool that generates highly personalized emails based on contact information

## Features

### UI Front-End

- **Contact Management**: Create, view, edit, and organize contacts
- **Folder Organization**: Group contacts into logical folders
- **Campaign Management**: Create and track outreach campaigns
- **Agent Configuration**: Set up and manage AI agents through a dedicated interface
- **Data Enrichment**: Enrich selected contacts with the integrated Researcher Agent
- **Template Management**: Create, edit, and manage email templates for personalization
- **Email Personalization**: Generate highly personalized emails using AI

### Researcher Agent

- **CSV Processing**: Intelligently processes contact information from CSV files
- **Web Research**: Searches for company information using DuckDuckGo
- **Contact Extraction**: Extracts contact information from company websites
- **Social Media Discovery**: Finds company social media profiles
- **News Aggregation**: Collects recent news about companies
- **AI Summary Generation**: Creates concise summaries using:
  - Google's Gemini AI
  - OpenRouter (supporting Claude, GPT-4, Mistral, Llama and more)

### Personalizor Agent

- **Email Personalization**: Generates highly personalized emails based on company information
- **Template Management**: Saves and manages reusable email templates
- **Batch Processing**: Processes multiple contacts in batches for efficient personalization
- **Confidence Scoring**: Calculates personalization quality scores for generated emails
- **Multiple AI Models**: Supports both Google Gemini and OpenRouter (Claude, GPT-4, etc.)
- **Customizable Settings**: Configure tone, length, call-to-action, and personalization level

## System Requirements

- Node.js 14+ (for UI Front-End)
- Python 3.7+ (for Researcher Agent)
- Python 3.10+ (for Personalizor Agent)
- One of the following API keys:
  - Google Gemini API key
  - OpenRouter API key
- Firecrawl API key (optional)
- Supabase account (for database storage)

## Quick Start

### Installation

1. Clone this repository
2. Install dependencies for all components:

```bash
# Install everything with one command
npm run install-all

# Or install components separately
npm run install-ui       # Install UI Front-End dependencies
npm run install-agent    # Install Researcher Agent dependencies
npm run install-personalizor # Install Personalizor Agent dependencies
```

3. Set up your environment variables:

   Create a `.env` file in the root directory with:

   ```
   PORT=5000
   NODE_ENV=development
   ```

   Configure the Researcher Agent and Personalizor Agent through the Agents tab in the UI.

### Starting the Application

Run the entire application with a single command from the root directory:

```bash
npm start
```

This will:
1. Check and install any missing dependencies
2. Build the React app if needed
3. Find an available port automatically (if port 5000 is already in use)
4. Start the Express server that serves both the API and React app

You'll see a message with the URL where you can access the application, such as:
```
You can access the application at: http://localhost:5001
```

## Development Mode

For faster development with hot-reloading (changes appear instantly without rebuilding), use our development mode:

```bash
npm run dev
```

This will:
1. Start the Express server (API + Researcher Agent) on an available port
2. Start the React development server with hot reloading
3. Configure the React dev server to proxy API requests to the Express server

Once running, you can:
- Access the UI with hot reloading at **http://localhost:3000**
- Make changes to React components and see them instantly without rebuilding
- Use all API features including the Researcher Agent
- Press Ctrl+C to shut down both servers

### When to Use Development Mode vs. Production Mode

- **Development Mode** (`npm run dev`): 
  - Use during active development
  - Changes to UI code appear instantly
  - Full API access including Researcher Agent integration
  - Best for rapid UI iteration

- **Production Mode** (`npm start` or `npm run rebuild`):
  - Use for testing the production build
  - Changes require rebuilding the app
  - More closely represents the deployed application
  - Required for testing server-side rendering or optimizations

## Making Changes

### When to Rebuild the App

After making any changes to the UI code (files in UI_FrontEnd/src), you need to rebuild the app for changes to appear in production mode:

```bash
# One-step rebuild and restart (recommended)
npm run rebuild

# Or manually:
cd UI_FrontEnd
npm run build
cd ..
npm start
```

### Development Workflow

For faster development:

1. **Option 1: Use development mode with hot reloading** (fastest)
   ```bash
   npm run dev
   ```
   Then make changes to UI files and see them instantly at http://localhost:3000

2. **Option 2: Use the rebuild script** (for production testing)
   ```bash
   # After making changes:
   npm run rebuild
   ```

The development mode eliminates the need to rebuild after each change, making your development process much faster while still maintaining full integration with the API and Researcher Agent.

## Architecture

```
AIBDR/
├── UI_FrontEnd/                 # Front-end React application
│   ├── public/                  # Static assets
│   ├── src/                     # Source code
│   │   ├── components/          # Reusable UI components
│   │   ├── contexts/            # React contexts for state management
│   │   ├── pages/               # Page components
│   │   │   ├── Agent/           # Agent configuration UI
│   │   │   ├── Campaign/        # Campaign management UI
│   │   │   ├── Contacts/        # Contact management UI
│   │   │   ├── Dashboard/       # Dashboard UI
│   │   │   ├── Folders/         # Folder management UI
│   │   │   └── Templates/       # Template management UI
│   │   ├── services/            # API services
│   │   └── utils/               # Utility functions
│   ├── server/                  # Express server
│   │   ├── routes/              # API routes
│   │   └── agents/              # Agent integrations
│   └── package.json             # Node.js dependencies
│
├── Researcher Agent/            # Python-based research agent
│   ├── ai_agent.py              # Main agent code
│   ├── tools/                   # Research and extraction tools
│   │   ├── duckduckgo.py        # Web search functionality
│   │   ├── firecrawl.py         # Contact extraction via API
│   │   └── crawl4ai.py          # Browser-based extraction
│   ├── tests/                   # Testing utilities for connections
│   │   ├── test_supabase.py     # Test Supabase connectivity
│   │   └── test_find_contact.py # Test contact retrieval
│   ├── logs/                    # Log files directory
│   ├── requirements.txt         # Python dependencies
│   └── .env                     # Agent configuration
│
├── PersonalizorAgent/           # Python-based personalization agent
│   ├── personalizor_agent.py    # Main agent code
│   ├── models.py                # Data models
│   ├── bridge/                  # Bridge scripts for Node.js integration
│   │   ├── personalize_email.py # Single email personalization
│   │   ├── process_batch.py     # Batch processing
│   │   ├── get_templates.py     # Template retrieval
│   │   ├── save_template.py     # Template saving
│   │   └── delete_template.py   # Template deletion
│   ├── logs/                    # Log files directory
│   ├── requirements.txt         # Python dependencies
│   └── .env                     # Agent configuration
│
├── package.json                 # Root package.json for starting everything
└── README.md                    # This documentation
```

## Configuration

### UI Front-End

Configuration is managed through the `.env` file in the root directory:

```
PORT=5000              # Server port (will auto-detect if in use)
NODE_ENV=development   # Environment
```

### Researcher Agent

The Researcher Agent can be configured through:

1. The **Agents** tab in the UI (recommended)
2. Directly editing the `.env` file in the `Researcher Agent` directory:

```
GEMINI_API_KEY=your_key_here
BATCH_SIZE=2
BATCH_COOLDOWN_SECONDS=15
SEARCH_DELAY_SECONDS=2
FIRECRAWL_API_KEY=your_key_here
ENABLE_DUCKDUCKGO=true
ENABLE_FIRECRAWL=false
```

### Personalizor Agent

The Personalizor Agent can be configured through:

1. The **Agents** tab in the UI (recommended)
2. Directly editing the `.env` file in the `PersonalizorAgent` directory:

```
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL=gemini-1.5-pro
# OR
OPENROUTER_API_KEY=your_openrouter_api_key
OPENROUTER_MODEL=anthropic/claude-3-opus:beta
AI_PROVIDER=gemini  # or "openrouter"

# Default settings
DEFAULT_TONE=professional
DEFAULT_LENGTH=medium
DEFAULT_CTA=meeting
DEFAULT_PERSONALIZATION_LEVEL=high

# Supabase settings (for storing templates and results)
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
```

## Development

### UI Front-End

Run the front-end only in development mode:

```bash
cd UI_FrontEnd
npm run start
```

### Researcher Agent

Run the Researcher Agent directly:

```bash
cd "Researcher Agent"
python ai_agent.py
```

### Personalizor Agent

Run the Personalizor Agent directly:

```bash
cd PersonalizorAgent
python personalizor_agent.py
```

## API Endpoints

The API is served from the Express server and includes:

### Researcher Agent Endpoints
- **GET /api/researcher/status**: Check the status of the Researcher Agent
- **POST /api/researcher/enrich**: Enrich contacts with the Researcher Agent
- **GET /api/researcher/config**: Get the Researcher Agent configuration
- **POST /api/researcher/config**: Save the Researcher Agent configuration

### Personalizor Agent Endpoints
- **GET /api/personalizor/status**: Check the status of the Personalizor Agent
- **POST /api/personalizor/personalize**: Generate a personalized email
- **POST /api/personalizor/personalize-batch**: Process a batch of contacts
- **GET /api/personalizor/templates**: Get all prompt templates
- **POST /api/personalizor/templates**: Save a prompt template
- **DELETE /api/personalizor/templates/:id**: Delete a prompt template
- **GET /api/personalizor/config**: Get the Personalizor Agent configuration
- **POST /api/personalizor/config**: Save the Personalizor Agent configuration

## Troubleshooting

If you encounter issues:

1. **Missing dependencies**: Run `npm run install-all` to ensure all dependencies are installed
2. **Python errors**: Ensure Python 3.7+ is installed and available in your PATH
3. **API key issues**: Check that you've configured the Gemini API key or OpenRouter API key in the Agents tab
4. **Connection errors**: Ensure the server is running (check the console for the exact port)
5. **Port conflicts**: The application will automatically find an available port if 5000 is in use
6. **Changes not appearing in production mode**: After modifying UI code, rebuild the app using `npm run rebuild`
7. **Changes not appearing in development mode**: If using `npm run dev`, refresh the browser if needed
8. **DuckDuckGo search errors**: If you see errors like `unexpected keyword argument 'proxies'`, this indicates a version compatibility issue - update the DuckDuckGo search tool
9. **Crawl4AI extraction errors**: If you encounter `'CrawlResult' object has no attribute` errors, this is due to API changes in newer versions - update the Crawl4AI tool accordingly
10. **Rate limiting with Gemini**: The system implements exponential backoff for rate limits, but you may need to slow down processing by reducing batch sizes if you hit persistent rate limits. Alternatively, switch to OpenRouter as your AI provider.
11. **Missing Playwright browser executables**: If using Crawl4AI and seeing browser errors, run `python -m playwright install` to install required browsers
12. **Supabase connectivity issues**: If contacts aren't being updated in Supabase, use the testing tools in the `Researcher Agent/tests/` directory to diagnose connection and permission issues:
    - `python Researcher\ Agent/tests/test_supabase.py` - Test basic Supabase connectivity
    - `python Researcher\ Agent/tests/test_supabase_update.py` - Test contact update functionality
    - `python Researcher\ Agent/tests/test_list_all_contacts.py` - List existing contacts
    - `python Researcher\ Agent/tests/test_find_contact.py <contact_id>` - Find a specific contact
13. **OpenRouter connectivity issues**: If you're using OpenRouter and experiencing issues, test your configuration with:
    - `python Researcher\ Agent/tests/test_openrouter.py` - Test OpenRouter connectivity and model response

### Monitoring Logs

For detailed troubleshooting:

1. Check log files in the `Researcher Agent/logs/` directory (named with timestamps)
2. Use `cd Researcher\ Agent && tail -f logs/ai_agent_$(ls -t logs/ | head -1)` to view the latest logs in real-time
3. If a specific tool is failing, look for log entries with that tool's name (e.g., "Crawl4AI", "Firecrawl", "DuckDuckGo")
4. For Supabase issues, the testing tools provide detailed error feedback and can help isolate connectivity or authentication problems

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -am 'Add my feature'`
4. Push to the branch: `git push origin feature/my-feature`
5. Submit a pull request

## License

[Specify your license here] 
