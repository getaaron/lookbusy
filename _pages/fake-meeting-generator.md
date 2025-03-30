---
layout: page
title: Fake Meeting Generator
include_in_header: true
---

<div class="meeting-generator-container">
  <h1>Fake Meeting Generator</h1>
  
  <div class="generator-form">
    <div class="form-group">
      <label for="jobTitle">Job Title</label>
      <input type="text" id="jobTitle" placeholder="Enter your job title (e.g., Software Engineer, Product Manager)" class="form-control">
    </div>
    
    <button id="generateButton" class="generate-button">Generate Fake Meeting</button>
  </div>
  
  <div id="results" class="results-container hidden">
    <h3>Your Generated Meeting Titles</h3>
    <ul id="meetingsList" class="meetings-list"></ul>
    <button id="generateMore" class="secondary-button">Generate More</button>
    <button id="clearResults" class="secondary-button">Clear</button>
  </div>
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const jobTitleInput = document.getElementById('jobTitle');
    const generateButton = document.getElementById('generateButton');
    const generateMoreButton = document.getElementById('generateMore');
    const clearResultsButton = document.getElementById('clearResults');
    const resultsContainer = document.getElementById('results');
    const meetingsList = document.getElementById('meetingsList');
    
    // Meeting templates
    const meetingTemplates = {
      general: [
        "Weekly Status Update",
        "Quarterly Planning",
        "Team Sync",
        "Project Kickoff",
        "Strategic Alignment",
        "One-on-One with Manager",
        "Cross-team Collaboration",
        "Performance Review",
        "Department All-Hands",
        "Budget Review"
      ],
      
      tech: [
        "Sprint Planning",
        "Code Review",
        "Architecture Discussion",
        "Tech Debt Cleanup",
        "Release Planning",
        "DevOps Strategy",
        "Security Review",
        "API Design Session",
        "Database Optimization",
        "System Integration Meeting"
      ],
      
      product: [
        "Product Roadmap Review",
        "Feature Prioritization",
        "User Research Debrief",
        "Stakeholder Feedback",
        "UX Design Review",
        "Market Analysis",
        "Competitor Review",
        "Product Launch Planning",
        "A/B Test Results",
        "Customer Journey Mapping"
      ],
      
      management: [
        "Leadership Sync",
        "Resource Allocation",
        "Team Performance Review",
        "OKR Setting",
        "Strategic Initiative Planning",
        "Budget Approval",
        "Risk Assessment",
        "Talent Development",
        "Org Structure Planning",
        "Executive Briefing"
      ],
      
      marketing: [
        "Campaign Strategy",
        "Content Calendar Review",
        "Analytics Review",
        "Brand Positioning",
        "Social Media Planning",
        "Marketing Budget Review",
        "SEO Strategy",
        "Email Marketing Planning",
        "Creative Review",
        "Conversion Optimization"
      ]
    };
    
    // Function to generate a meeting title based on job title
    function generateMeetingTitle(jobTitle) {
      let relevantTemplates = [...meetingTemplates.general];
      
      // Add job-specific templates
      const jobLower = jobTitle.toLowerCase();
      
      if (jobLower.includes('engineer') || jobLower.includes('developer') || jobLower.includes('programmer') || 
          jobLower.includes('architect') || jobLower.includes('tech') || jobLower.includes('data')) {
        relevantTemplates = relevantTemplates.concat(meetingTemplates.tech);
      }
      
      if (jobLower.includes('product') || jobLower.includes('manager') || jobLower.includes('owner') || 
          jobLower.includes('ux') || jobLower.includes('ui') || jobLower.includes('design')) {
        relevantTemplates = relevantTemplates.concat(meetingTemplates.product);
      }
      
      if (jobLower.includes('manager') || jobLower.includes('director') || jobLower.includes('lead') || 
          jobLower.includes('head') || jobLower.includes('chief') || jobLower.includes('vp') || 
          jobLower.includes('president')) {
        relevantTemplates = relevantTemplates.concat(meetingTemplates.management);
      }
      
      if (jobLower.includes('market') || jobLower.includes('content') || jobLower.includes('brand') || 
          jobLower.includes('social') || jobLower.includes('communications') || jobLower.includes('pr')) {
        relevantTemplates = relevantTemplates.concat(meetingTemplates.marketing);
      }
      
      // Pick a random template
      const randomTemplate = relevantTemplates[Math.floor(Math.random() * relevantTemplates.length)];
      
      // Sometimes add a specific context to make it more realistic
      const contexts = [
        `for ${jobTitle}s`,
        "with Stakeholders",
        "with Leadership",
        "- Urgent",
        "- Follow-up",
        `- Q${Math.floor(Math.random() * 4) + 1}`,
        "Discussion",
        "Workshop",
        "Committee",
        "Working Group"
      ];
      
      // 50% chance to add a context
      if (Math.random() > 0.5) {
        return `${randomTemplate} ${contexts[Math.floor(Math.random() * contexts.length)]}`;
      }
      
      return randomTemplate;
    }
    
    // Generate multiple meeting titles
    function generateMeetings(jobTitle, count = 5) {
      const meetings = [];
      for (let i = 0; i < count; i++) {
        meetings.push(generateMeetingTitle(jobTitle));
      }
      return meetings;
    }
    
    // Display generated meetings
    function displayMeetings(meetings) {
      meetings.forEach(meeting => {
        const li = document.createElement('li');
        li.textContent = meeting;
        meetingsList.appendChild(li);
      });
      
      resultsContainer.classList.remove('hidden');
    }
    
    // Event listeners
    generateButton.addEventListener('click', function() {
      const jobTitle = jobTitleInput.value.trim() || 'Professional';
      meetingsList.innerHTML = ''; // Clear existing meetings
      const meetings = generateMeetings(jobTitle);
      displayMeetings(meetings);
    });
    
    generateMoreButton.addEventListener('click', function() {
      const jobTitle = jobTitleInput.value.trim() || 'Professional';
      const meetings = generateMeetings(jobTitle, 3);
      displayMeetings(meetings);
    });
    
    clearResultsButton.addEventListener('click', function() {
      meetingsList.innerHTML = '';
      resultsContainer.classList.add('hidden');
    });
  });
</script>

<style>
  .meeting-generator-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }
  
  .generator-form {
    margin: 2rem 0;
  }
  
  .form-group {
    margin-bottom: 1.5rem;
  }
  
  label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: bold;
  }
  
  .form-control {
    width: 100%;
    padding: 0.75rem;
    font-size: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-bottom: 1rem;
  }
  
  .generate-button {
    display: block;
    width: 100%;
    background-color: #1d63ea;
    color: white;
    font-size: 1.2rem;
    padding: 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .generate-button:hover {
    background-color: #1850c0;
  }
  
  .results-container {
    margin-top: 2rem;
    padding: 1.5rem;
    border: 1px solid #eee;
    border-radius: 4px;
    background-color: #f9f9f9;
  }
  
  .results-container.hidden {
    display: none;
  }
  
  .meetings-list {
    list-style-type: none;
    padding: 0;
    margin: 1rem 0;
  }
  
  .meetings-list li {
    padding: 0.75rem;
    margin-bottom: 0.5rem;
    background-color: white;
    border: 1px solid #eee;
    border-radius: 4px;
  }
  
  .secondary-button {
    padding: 0.5rem 1rem;
    margin-right: 0.5rem;
    background-color: #f5f5f5;
    border: 1px solid #ddd;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .secondary-button:hover {
    background-color: #e5e5e5;
  }
</style> 