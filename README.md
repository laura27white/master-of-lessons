# Master of Lessons - Ghosts of Projects Past

**An intelligent lessons learned library and SME agent for MOD Gateway Reviews**

Transform your project gateway reviews into actionable insights with automated lesson extraction, categorization, and AI-powered recommendations. This web application helps Project Managers, SROs, and Reviewers discover patterns, avoid recurring issues, and apply lessons learned to current projects.

---

## What This Tool Does

**Master of Lessons** is a comprehensive platform designed to address the challenge of lessons learned getting lost after project reviews. It provides:

1. **Automated Lesson Extraction**: Pre-populate lessons directly from Gateway review documents
2. **Intelligent Categorization**: Automatically organize lessons by theme (procurement, governance, resourcing, risk, delivery)
3. **Ghost Detection**: Identify recurring problems ("ghosts") that haunt multiple projects
4. **Visual Analytics**: Radar charts and insights showing project health across key dimensions
5. **Searchable Library**: Powerful search and filtering to find relevant lessons for your context
6. **Automated Recommendations**: Guidance on applying lessons to current project situations

This tool serves two main use cases:
- **Branch 1**: Core Lessons Library - A structured repository for searching, filtering, and reusing lessons
- **Branch 2**: Lessons SME Agent - An intelligent system providing tailored advice like a digital subject matter expert

---

## Quick Start

### Prerequisites

- Node.js 16+ ([Download here](https://nodejs.org/))
- npm (comes with Node.js)
- A text editor (VS Code recommended)

### Installation

1. **Clone the repository**:
```bash
git clone https://github.com/laura27white/master-of-lessons
cd master-of-lessons
```

2. **Install dependencies**:
```bash
npm install
```

3. **Run the development server**:
```bash
npm run dev
```

4. **Open your browser** to `http://localhost:5173`

That's it! The demo application is now running with sample MOD Gateway Review data.

---

## Setting Up Your Own Database

Want to use this with your own project documents? Follow these steps:

### Step 1: Understand the Data Format

The application reads JSON files from the `/data` directory. Each project document should follow this structure:

```json
{
  "projectName": "Your Project Name",
  "projectCode": "PROJ-001",
  "gateway": "Gate 0/4 hybrid",
  "date": "2021-07",
  "status": "Conditional",
  "reviewId": "GR-2021-001",
  "deliveryConfidenceAssessment": "Amber/Green",
  "keyDecisions": [
    "Decision 1",
    "Decision 2"
  ],
  "risks": [
    "Risk description 1",
    "Risk description 2"
  ],
  "actions": [
    "Action item 1",
    "Action item 2"
  ],
  "lessonsLearned": [
    "Lesson 1 text",
    "Lesson 2 text"
  ],
  "metadata": {
    "documentType": "MOD Integrated Assurance Gate Review Report",
    "previousReviews": [],
    "totalPages": 25
  }
}
```

### Step 2: Prepare Your Data

1. **Create JSON files**: Convert your gateway review documents into JSON format following the structure above
   - You can split data across multiple files (the app currently uses 3 files)
   - Each file should contain an array of project objects

2. **Place files in the data directory**:
```bash
data/
├── your_projects_1.json
├── your_projects_2.json
└── your_projects_3.json
```

### Step 3: Update the Data Loader

Edit `src/utils/data.js` to import your JSON files:

```javascript
// Replace these imports with your own files
import projectsData1 from '../../data/your_projects_1.json'
import projectsData2 from '../../data/your_projects_2.json'
import projectsData3 from '../../data/your_projects_3.json'

// Combine data from all JSON files
export const projects = [...projectsData1, ...projectsData2, ...projectsData3]
```

### Step 4: Customize Categories (Optional)

The lesson categorization logic is in `src/utils/data.js` in the `categorizeLesson()` function. You can customize it to match your organization's taxonomy:

```javascript
export const categorizeLesson = (text) => {
  const lower = text.toLowerCase()
  if (lower.includes('resource') || lower.includes('staff')) {
    return 'Resource Management'
  }
  // Add your own categories and keywords
  if (lower.includes('your-keyword')) {
    return 'Your Custom Category'
  }
  return 'General'
}
```

### Step 5: Test Your Setup

1. **Restart the development server**:
```bash
npm run dev
```

2. **Verify your data loads**: Check the Dashboard for your project count
3. **Test the Lessons Library**: Search and filter your lessons
4. **View Insights**: Check that analytics display correctly

---

## Features Guide

### Dashboard
- **Overview Metrics**: Total projects, lessons, and project health indicators
- **DCA Distribution**: Visual breakdown of Delivery Confidence Assessments
- **Recent Projects**: Quick access to latest gateway reviews

### Lessons Library
- **Advanced Search**: Full-text search across all lessons
- **Multi-Filter**: Filter by category, DCA rating, project, and date range
- **Export**: Download filtered results as CSV for offline analysis
- **Quick View**: See lesson context (project, gateway, date) at a glance

### Insights & Analytics
- **Lessons by Category**: Bar chart showing distribution across themes
- **Trend Analysis**: Timeline of projects and DCA ratings
- **Top Themes**: Most frequently occurring keywords and issues
- **Radar Analytics**: Multi-dimensional project health assessment

### Ghost Detection
The "Ghost Detector" radar identifies recurring problems across projects:
- Resource Ghosts (staffing, SQEP shortages)
- Commercial Ghosts (contract issues, supplier problems)
- Schedule Ghosts (delays, timeline slippage)
- Governance Ghosts (decision-making, board issues)
- Capability Ghosts (skills gaps, expertise)
- Integration Ghosts (dependencies, coordination)

### Project Details
Click any project to see:
- Full gateway review summary
- All key decisions, risks, and actions
- Complete lessons learned with context
- Project health radar across 6 dimensions

---

## Deployment

### Deploy to Netlify (Recommended)

**Option 1: Netlify CLI**
```bash
npm install -g netlify-cli
netlify login
npm run build
netlify deploy --prod
```

**Option 2: GitHub + Netlify UI**
1. Push your code to GitHub
2. Connect repository to [Netlify](https://app.netlify.com)
3. Netlify auto-detects build settings from `netlify.toml`
4. Click "Deploy site"

**Option 3: Drag & Drop**
```bash
npm run build
# Drag the 'dist' folder to https://app.netlify.com/drop
```

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed deployment instructions and other hosting options.

---

## Technology Stack

- **React 18**: Modern UI framework
- **Vite**: Lightning-fast build tool
- **React Router**: Client-side routing
- **Recharts**: Data visualization and radar charts
- **Lucide React**: Icon library

---

## Project Structure

```
master-of-lessons/
├── data/                          # JSON data files
│   ├── mod_gateway_docs_1_2_3_4_5_6.json
│   ├── mod_gateway_docs_7_8.json
│   └── mod_gateway_docs_9_10.json
├── src/
│   ├── components/                # Reusable React components
│   │   ├── Navigation.jsx
│   │   ├── MetricCard.jsx
│   │   ├── FernDecoration.jsx
│   │   └── RadarAnalytics.jsx
│   ├── pages/                     # Main application pages
│   │   ├── Dashboard.jsx
│   │   ├── LessonsLibrary.jsx
│   │   ├── Insights.jsx
│   │   └── ProjectDetail.jsx
│   ├── utils/
│   │   └── data.js               # Data processing & analytics logic
│   ├── App.jsx                    # Main app component
│   └── index.css                  # Global styles
├── public/                        # Static assets
├── netlify.toml                   # Deployment configuration
└── package.json                   # Dependencies and scripts
```

---

## Customization

### Branding & Theme
- Edit colors in `src/index.css` (CSS variables at the top)
- Update navigation labels in `src/components/Navigation.jsx`
- Change page titles and descriptions in individual page components

### Analytics Logic
- Modify radar chart calculations in `src/utils/data.js`
- Add new analytics functions following existing patterns
- Update chart components in `src/pages/Insights.jsx`

### Additional Features
The codebase is designed for easy extension:
- Add new filtering options in `LessonsLibrary.jsx`
- Create new visualization types in `Insights.jsx`
- Extend the categorization logic in `data.js`

---

## Data Privacy & Security

This application runs entirely in the browser with **no backend server**. All data is:
- Stored as static JSON files
- Processed client-side
- Never sent to external servers

For sensitive data:
- Deploy to a private/authenticated hosting environment
- Use access controls at the hosting level
- Remove or anonymize sensitive information in JSON files

---

## Contributing

Contributions welcome! Areas for improvement:
- Natural language processing for better lesson categorization
- Integration with document management systems
- More sophisticated recommendation algorithms
- AI-powered lesson similarity matching
- Multi-language support

---

## Support & Documentation

- **Issues**: Report bugs at [GitHub Issues]([https://github.com/laura27white/master-of-lessons])
- **Documentation**: See [DEPLOYMENT.md](./DEPLOYMENT.md) for deployment details
- **Judges**: See [JUDGES.md](./JUDGES.md) for hackathon submission details

---

## License

MOD Gateway Reviews Data Visualization Tool - Hackathon Project 2025

---

*"Gimme Fuel Gimme Fire Give Me That Lesson I Desire"* 🎸🐱🌿

**Built with ❤️ for better project delivery through lessons learned**
