# DSA Problems Search Engine 🔍

A full-stack web application that provides intelligent search capabilities for Data Structures and Algorithms (DSA) problems. Built with Node.js, Express, MongoDB, and vanilla JavaScript, this search engine uses TF-IDF (Term Frequency-Inverse Document Frequency) algorithm to deliver relevant search results.

## 🌟 Features

- **Intelligent Search**: TF-IDF based search algorithm for accurate results
- **Advanced Filtering**: Filter by difficulty level and problem tags
- **Real-time Search**: Fast and responsive search experience
- **Problem Database**: Comprehensive collection of DSA problems from various platforms
- **Clean UI**: Simple and intuitive user interface
- **RESTful API**: Well-structured API endpoints for extensibility

## 🛠️ Tech Stack

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web application framework
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling
- **CORS** - Cross-origin resource sharing

### Frontend
- **HTML5** - Markup language
- **CSS3** - Styling and responsive design
- **Vanilla JavaScript** - Client-side functionality

### Search Algorithm
- **TF-IDF** - Term Frequency-Inverse Document Frequency for relevance scoring

## 📁 Project Structure

```
├── backend/
│   ├── App/
│   │   └── models/
│   │       └── questionSchema.js    # MongoDB schema for problems
│   ├── create_database.js           # Database setup and population script
│   ├── index.js                     # Main server file
│   └── package.json                 # Backend dependencies
├── Frontend/
│   ├── index.html                   # Main HTML file
│   ├── script.js                    # Client-side JavaScript
│   └── styles.css                   # CSS styles
├── precompute/
│   ├── app.js                       # TF-IDF search implementation
│   ├── indexer.js                   # Index generation for search
│   ├── names.txt                    # Problem titles
│   ├── url.txt                      # Problem URLs
│   ├── data/                        # Problem data files
│   │   ├── 0.txt
│   │   ├── 1.txt
│   │   └── ...                      # Individual problem files
│   └── index/                       # Generated search indices
├── package.json                     # Root dependencies
└── README.md                        # Project documentation
```

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed on your system:
- [Node.js](https://nodejs.org/) (version 14 or higher)
- [MongoDB](https://www.mongodb.com/) (local installation or MongoDB Atlas)
- [Git](https://git-scm.com/)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/lazy-coder99/CrossPlatform-DSA-Problems-SearchEngine/tree/main
   cd CrossPlatform-DSA-Problems-SearchEngine
   ```

2. **Install root dependencies**
   ```bash
   npm install
   ```

3. **Install backend dependencies**
   ```bash
   cd backend
   npm install
   ```

4. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```bash
   touch .env
   ```
   
   Add the following variables to `.env`:
   ```env
   MONGOOSE_URL=mongodb://localhost:27017/dsa-search-engine
   PORT=3000
   ```
   
   **For MongoDB Atlas (cloud database):**
   ```env
   MONGOOSE_URL=mongodb+srv://username:password@cluster.mongodb.net/dsa-search-engine
   PORT=3000
   ```

### 🗄️ Database Setup

1. **Generate search indices** (from the root directory):
   ```bash
   cd precompute
   node indexer.js
   ```

2. **Populate the database** (from the backend directory):
   ```bash
   cd backend
   node create_database.js
   ```

### 🏃 Running the Application

1. **Start the server** (from the backend directory):
   ```bash
   cd backend
   npm start
   ```
   
   Or using Node directly:
   ```bash
   node index.js
   ```

2. **Access the application**
   
   Open your browser and navigate to:
   ```
   http://localhost:3000
   ```

## 📋 API Endpoints

### Search Problems
```http
GET /api/search?user_query=<query>&difficulty=<level>&tags=<tag1,tag2>
```

**Parameters:**
- `user_query` (required): Search query string
- `difficulty` (optional): Filter by difficulty (Easy, Medium, Hard)
- `tags` (optional): Comma-separated list of tags

**Example:**
```bash
curl "http://localhost:3000/api/search?user_query=binary%20tree&difficulty=Medium&tags=tree,recursion"
```

### Add New Problem
```http
POST /api/problems-insert
```

**Request Body:**
```json
{
  "title": "Two Sum",
  "description": "Find two numbers that add up to target",
  "difficulty": "Easy",
  "tags": ["array", "hash-table"],
  "url": "https://leetcode.com/problems/two-sum/",
  "platform": "LeetCode"
}
```

## 🔧 Configuration

### MongoDB Configuration

**Local MongoDB:**
```env
MONGOOSE_URL=mongodb://localhost:27017/dsa-search-engine
```

**MongoDB Atlas:**
1. Create a cluster on [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Get your connection string
3. Replace the `MONGOOSE_URL` in `.env` file

### Port Configuration

Change the port in `.env` file:
```env
PORT=5000
```

## 📊 Data Format

### Problem Data Files (`precompute/data/*.txt`)

Each problem file follows this format:
```
Easy
array,hash-table,two-pointers
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
```

**Format:**
- Line 1: Difficulty level
- Line 2: Comma-separated tags
- Line 3+: Problem description

Live Demo Link : https://mern-dsa-search-engine.onrender.com/
### Names and URLs (`precompute/names.txt` and `precompute/url.txt`)

- `names.txt`: One problem title per line
- `url.txt`: Corresponding problem URLs (same line number as names.txt)


## 🤝 Contributing

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add some amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

## 📝 Adding New Problems

1. **Add problem data file** in `precompute/data/` directory (e.g., `301.txt`)
2. **Add problem title** to `precompute/names.txt`
3. **Add problem URL** to `precompute/url.txt`
4. **Regenerate indices**:
   ```bash
   cd precompute
   node indexer.js
   ```
5. **Update database**:
   ```bash
   cd backend
   node create_database.js
   ```

## 🐛 Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Ensure MongoDB is running locally
   - Check the `MONGOOSE_URL` in `.env` file
   - Verify network access for MongoDB Atlas

2. **Port Already in Use**
   - Change the port in `.env` file
   - Kill the process using the port: `sudo lsof -t -i:3000 | xargs kill -9`

3. **Search Not Working**
   - Ensure indices are generated: `cd precompute && node indexer.js`
   - Check if database is populated: `cd backend && node create_database.js`

4. **Empty Search Results**
   - Verify problem data files exist in `precompute/data/`
   - Check MongoDB connection and data
