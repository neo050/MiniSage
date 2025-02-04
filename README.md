
# MiniSage

**MiniSage** is a dynamic, modular website dedicated to comparing used mini and sub-mini cars (up to 25,000 ₪). Powered by a smart AI integration, MiniSage automatically analyzes market data and updates its recommendations, ensuring that users always see current trends and insights.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [File Structure](#file-structure)
- [Installation](#installation)
- [Usage](#usage)
  - [Running the API Server](#running-the-api-server)
  - [Running the Update Script](#running-the-update-script)
  - [Frontend](#frontend)
- [Environment Variables](#environment-variables)
- [Deployment Considerations](#deployment-considerations)
- [Database Considerations](#database-considerations)
- [Contributing](#contributing)
- [License](#license)

## Overview

**MiniSage** is designed as a global, publicly accessible website that:
- Uses modular HTML, CSS, and JavaScript to ensure maintainability and scalability.
- Fetches data and AI-generated analysis through a backend API built with Node.js and Express.
- Automatically updates car market data and insights using a scheduled update script and AI integration via the OpenAI API.
- Is easily extendable—currently, data is stored in JSON files, but the architecture supports integration with a full database if needed.

## Features

- **Modular Frontend:**  
  - Separation of concerns with dedicated files for HTML, CSS, and JavaScript (ES6 modules).
  - Responsive and accessible design with RTL support for Hebrew.

- **Backend API:**  
  - Built with Node.js and Express.
  - Exposes endpoints to deliver the latest car data and AI-generated analysis.

- **AI Integration:**  
  - Utilizes OpenAI's GPT API to analyze market data and provide updated recommendations.
  - Scheduled updates keep data and insights current.

- **Data Storage:**  
  - Uses JSON files (`/data/cars.json` and `/data/analysis.json`) to store data, with the option to migrate to a database for enhanced scalability.

## File Structure

```
/project-root
├── index.html                 # Main HTML file
├── README.md                  # This README file
├── /css
│   └── styles.css             # Main stylesheet
├── /js
│   ├── main.js                # Entry point for JavaScript
│   └── /modules
│       ├── table.js           # Module for building the car table
│       └── analysis.js        # Module for rendering the analysis section
├── /api
│   ├── server.js              # Express API server
│   └── aiService.js           # AI service integration (OpenAI API)
├── /data
│   ├── cars.json              # Car market data (sample; auto-updated)
│   └── analysis.json          # AI-generated analysis text (sample; auto-updated)
└── /cron
    └── updateData.js          # Script for updating data & running AI analysis (to be scheduled)
```

## Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/yourusername/minisage.git
   cd minisage
   ```

2. **Install Dependencies:**

   Ensure you have [Node.js](https://nodejs.org/) installed, then run:

   ```bash
   npm install express axios
   ```

3. **Set Environment Variables:**

   Create a `.env` file in the project root or set your environment variables in your hosting environment. You must set:

   ```bash
   OPENAI_API_KEY=your_openai_api_key_here
   PORT=3000
   ```

## Usage

### Running the API Server

Start the API server to serve data from the `/data` folder:

```bash
node api/server.js
```

This command starts an Express server on port 3000 (or the port specified by the `PORT` variable). The API provides the following endpoints:

- **GET `/api/cars`**: Returns the latest car data.
- **GET `/api/analysis`**: Returns the latest AI-generated analysis.

### Running the Update Script

To update car data and AI analysis, run the update script:

```bash
node cron/updateData.js
```

For production, schedule this script (using cron, Windows Task Scheduler, or a cloud scheduler) to run periodically (e.g., every 6 hours).

### Frontend

Open `index.html` in your browser. The frontend will:
- Dynamically fetch car data from `http://localhost:3000/api/cars`
- Dynamically fetch AI analysis from `http://localhost:3000/api/analysis`
- Render the comparison table and analysis sections accordingly.

If the backend is deployed on a different domain or port, adjust the API URLs in `/js/modules/table.js` and `/js/modules/analysis.js` accordingly.

## Environment Variables

This project requires:
- `OPENAI_API_KEY`: Your OpenAI API key.
- `PORT`: The port number for the API server (default is 3000).

## Deployment Considerations

- **Scalability:**  
  The stateless API server can be scaled horizontally behind a load balancer using cloud platforms such as AWS, Google Cloud, or Azure.

- **Security:**  
  Deploy the API with HTTPS, secure CORS policies, and proper HTTP security headers. In production, restrict CORS to your trusted domains.

- **Static Assets:**  
  Use a Content Delivery Network (CDN) to serve static files (HTML, CSS, JS) globally for enhanced performance.

- **Monitoring:**  
  Implement logging, monitoring, and error reporting for a robust production environment.

## Database Considerations

Currently, MiniSage stores data in JSON files for simplicity. For production use, consider integrating a robust database (e.g., PostgreSQL, MySQL, or MongoDB) for better scalability, data integrity, and concurrent access.

## Contributing

Contributions are welcome! Please fork the repository and submit pull requests for new features or bug fixes.

## License

This project is licensed under the [MIT License](LICENSE).

---

*Welcome to MiniSage – your intelligent guide to the world of used mini and sub-mini cars!*
```

---
