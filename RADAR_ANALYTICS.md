# Radar Diagram Analytics - Implementation Guide

## Overview
Comprehensive radar diagram analytics have been added to the Master of Lessons application, providing visual assessment of project health, risks, and recurring patterns across the MOD Gateway Review portfolio.

## Features Implemented

### 1. Project Health Assessment Radar
**Location:** Insights Page → Radar Analytics Section

**Purpose:** Compare projects across six key dimensions to identify weak areas visually.

**Dimensions:**
- Governance Maturity
- Resource Management
- Commercial Strategy
- Stakeholder Engagement
- Risk Management
- Schedule Control

**Scoring Algorithm:**
- Base score determined by DCA rating (RED: 40, Amber: 60, Amber/Green: 75, Green: 90)
- Score reduced by 8 points for each negative lesson in that dimension
- Minimum score of 20 ensures radar visibility
- Scores below 50 trigger warning indicators

**Usage:**
1. Navigate to Insights page
2. Select a project from dropdown
3. View six-dimensional health assessment
4. Check "Key Insights" section for critical areas

### 2. Lessons Category Distribution Radar
**Location:** Insights Page → Radar Analytics Section

**Purpose:** Show portfolio-wide thematic overview of recurring lessons for Portfolio Leads.

**Categories Tracked:**
- Resource Management
- Governance
- Technical Delivery
- Commercial Strategy
- Risk Management
- Stakeholder Relations

**Key Features:**
- Portfolio-wide aggregation
- Shows relative distribution across categories
- Identifies most common lesson themes
- Helps Portfolio Leads understand recurring patterns

### 3. Project Maturity Comparison Radar
**Location:** Insights Page → Radar Analytics Section

**Purpose:** Overlay multiple projects on one radar to identify patterns and systemic weaknesses.

**Capabilities:**
- Compare up to 4 projects simultaneously
- Visual pattern recognition across portfolio
- "Load Red-Rated Projects" quick action button
- Color-coded project lines for easy distinction
- DCA badge indicators for each project

**Use Cases:**
- Compare red-rated projects to identify common failure points
- Benchmark high-performing projects against struggling ones
- Identify systemic portfolio weaknesses
- Share best practices from high-scoring projects

### 4. Gateway Stage Risk Profile Radar
**Location:** Insights Page → Radar Analytics Section

**Purpose:** Analyze risk themes specific to gateway stages and projects.

**Risk Themes Tracked:**
- SQEP (Suitably Qualified & Experienced Personnel) Shortages
- Commercial Tensions
- Schedule Pressure
- Dependency Management
- Capability Ownership
- External Factors (COVID-19, geopolitical, supply chain)

**Data Sources:**
- Lessons learned text analysis
- Documented project risks
- Keyword frequency analysis

**Insights:**
- Top risk themes highlighted with occurrence counts
- Visual comparison of risk distribution
- Early warning system for emerging patterns

### 5. Ghost Detector Radar (Themed)
**Location:** Insights Page → Radar Analytics Section

**Purpose:** Show which "ghosts" (recurring problems) haunt each project with a themed visualization.

**Ghost Types:**
- 👻 Resource Ghosts (staffing issues)
- 👻 Commercial Ghosts (contract problems)
- 👻 Schedule Ghosts (timeline slippage)
- 👻 Governance Ghosts (leadership gaps)
- 👻 Capability Ghosts (SQEP shortages)
- 👻 Integration Ghosts (dependency issues)

**Severity Calculation:**
- Lessons Learned: 3 points each (highest weight)
- Documented Risks: 2 points each
- Actions Taken: 1 point each (indicates mitigation)
- Severity levels: High (>70%), Medium (40-70%), Low (<40%)

**Visual Features:**
- Purple-themed radar for "haunting" effect
- Severity warnings (⚠️) for high-impact ghosts
- Most haunting ghosts ranked in insights section

### 6. Portfolio Ghost Analysis
**Location:** Insights Page → Radar Analytics Section

**Purpose:** Aggregate all recurring problems across the entire portfolio.

**Features:**
- Portfolio-wide ghost severity scoring
- Identifies systemic problems affecting multiple projects
- Helps leadership prioritize improvement initiatives
- Shows which "ghosts" need organizational attention

## Technical Implementation

### Data Processing Functions (src/utils/data.js)
```javascript
// Core radar data functions
getProjectHealthRadar(projectCode)           // Returns 6-dimension health data
getLessonsCategoryRadar()                    // Returns portfolio category distribution
getProjectMaturityComparison(projectCodes)   // Returns multi-project comparison data
getGatewayStageRiskProfile(projectCode)      // Returns risk theme analysis
getGhostDetectorRadar(projectCode)           // Returns ghost severity data
getPortfolioGhostAnalysis()                  // Returns portfolio-wide ghost data

// Helper functions
calculateDimensionScore(lessons, keywords, baseScore)
countThemeOccurrences(lessons, risks, keywords)
detectGhost(lessons, risks, actions, keywords)
```

### Component Structure
- **RadarAnalytics.jsx** - Main container component
- **RadarAnalytics.css** - Complete styling including themed sections
- Integration with existing Recharts library

### Recharts Components Used
- RadarChart
- Radar (data layer)
- PolarGrid
- PolarAngleAxis
- PolarRadiusAxis
- Tooltip (custom styled)
- Legend
- ResponsiveContainer

## User Interface Features

### Interactive Controls
- **Project Selector**: Dropdown to select which project to analyze
- **Comparison Checkboxes**: Select up to 4 projects for comparison
- **Load Red Projects Button**: Quick-load red-rated projects
- **DCA Badges**: Visual indicators showing project health status

### Responsive Design
- Grid layout adapts to screen size
- Mobile-friendly controls
- Hover effects and tooltips
- Card-based design for easy scanning

### Visual Indicators
- Color-coded DCA badges (Red, Amber, Amber/Green, Green)
- Severity-based styling for ghosts
- Warning icons for critical insights
- Themed sections (purple for Ghost radars)

## Key Insights & Business Value

### For Project Managers
- Quick health assessment across six dimensions
- Identify weak areas requiring attention
- Compare against similar projects
- Track recurring issues (ghosts)

### For Portfolio Leads
- Thematic overview of recurring lessons
- Pattern recognition across projects
- Systemic weakness identification
- Resource allocation guidance

### For Senior Leadership
- Portfolio-wide risk visibility
- Data-driven decision support
- Common failure pattern identification
- Strategic improvement priorities

## Usage Examples

### Example 1: Analyzing a Red-Rated Project
1. Select red-rated project from dropdown
2. View Project Health Radar → identify lowest scoring dimensions
3. Check Risk Profile Radar → see which risk themes dominate
4. Review Ghost Detector → understand recurring problems
5. Use insights to guide intervention strategies

### Example 2: Portfolio-Wide Analysis
1. View Lessons Category Distribution → identify top categories
2. Load red-rated projects in Comparison Radar
3. Identify common low-scoring dimensions across projects
4. Check Portfolio Ghost Analysis → see systemic issues
5. Prioritize organizational improvements

### Example 3: Best Practice Sharing
1. Compare high-performing (Green) vs struggling (Red) projects
2. Identify dimensions where high-performers excel
3. Extract lessons from high-scoring projects
4. Share practices with struggling projects

## Color Palette

### DCA Colors
- RED: `#d45d5d`
- Amber: `#e8a84d`
- Amber/Green: `#8db896`
- Green: `#5f9e6e`

### Radar Colors
- Health Radar: Green (`#5f9e6e`, `#3d7a4c`)
- Category Radar: Amber (`#e8a84d`)
- Risk Profile: Red (`#d45d5d`)
- Ghost Detector: Purple (`#7c3aed`, `#9333ea`)

## Performance Considerations
- All calculations performed on-demand
- Efficient keyword matching algorithms
- Responsive design for smooth rendering
- Build size: 661KB (reasonable for feature-rich application)

## Future Enhancement Opportunities
1. **Time-series Analysis**: Track radar scores across gateway stages
2. **Export Functionality**: Download radar charts as images
3. **Threshold Alerts**: Email notifications when scores drop below thresholds
4. **Predictive Analytics**: ML models to predict future ghost occurrences
5. **Custom Dimensions**: Allow users to define custom radar dimensions
6. **Comparison History**: Save and compare radar states over time

## Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Responsive design (desktop, tablet, mobile)
- Recharts library compatibility: IE11+ (with polyfills)

## Maintenance Notes
- Keyword lists in data.js can be expanded for better categorization
- Scoring algorithms can be tuned based on user feedback
- Color schemes follow existing design system
- All radars use consistent fullMark scaling for comparability

---

**Built with:** React, Recharts, Vite
**Version:** 1.0.0
**Last Updated:** 2025-10-22
