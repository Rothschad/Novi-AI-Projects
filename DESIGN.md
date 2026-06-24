# Public Good App - Design Document

## Project Overview
**Name**: Public Good - Madrid Green Initiative  
**Purpose**: Aggregate community votes on quality-of-life improvements across Madrid districts and escalate validated ideas to local councils  
**Primary Users**: General public, local council members, community organizers  
**Geographic Scope**: All districts of Madrid  
**Timeline**: Complete by end of week (2026-06-28)  
**Team**: 2 people (no budget)

---

## Core Problem
Madrid residents lack an easy way to voice localized improvement suggestions (greenery, infrastructure, etc.). District-specific data isn't aggregated to identify city-wide patterns. Council engagement is unclear.

---

## Solution Overview
1. **Data Phase**: Analyze Madrid's public data (demographics, environmental data, council priorities) by district
2. **Question Generation**: Create data-driven, district-specific questions based on analysis
3. **Public Voting**: Users scan QR codes in their area, vote yes/no on suggestions, submit private feedback
4. **Threshold Logic**: Ideas reaching vote threshold by deadline escalate to council
5. **Fundraising**: GoFundMe-style donations unlock if idea passes threshold
6. **Admin Dashboard**: Web interface to view aggregated data, feedback, and manage campaigns

---

## User Flows

### Flow 1: Public User (Mobile App)
```
1. Scan QR code in physical location
2. See question + explanation of benefits
3. Vote Yes/No
4. (Optional) Submit private comment/feedback/question
5. (Optional) Share link with friends
6. Return to home or next question
```

### Flow 2: Admin/Data Analyst (Web Dashboard)
```
1. Login to admin dashboard
2. View aggregated voting data across all districts
3. See private comments/feedback (users can't see these)
4. Monitor thresholds in real-time
5. Escalate passed ideas to council
6. Manage GoFundMe campaigns (if threshold met)
```

### Flow 3: Council Member (Mobile/Web)
```
1. Receive notification of escalated idea
2. View public support, comments, funding
3. Respond/engage in conversation (attach to PR)
4. Track implementation status
```

---

## Core Features

### MVP (Mobile App - Phase 1)
- QR code scanner
- Vote submission (yes/no)
- Private comment box
- Share via link
- Simple UI (single screen per question)

### Admin Dashboard (Web - Phase 1)
- Login/authentication
- View all votes per district
- View private comments (searchable/filterable)
- Real-time vote counts
- Threshold status per question

### Phase 2 (If time)
- GoFundMe integration
- Council member dashboard
- Notification system
- Data analytics/heatmaps

---

## Data Model

### Questions Table
```
id, district, question_text, explanation, category, created_date, deadline, vote_threshold, status (active/passed/failed)
```

### Votes Table
```
id, question_id, user_ip (for deduplication), vote (yes/no), timestamp, district
```

### Comments Table
```
id, question_id, comment_text, feedback_type (comment/question/feedback), timestamp
```

---

## Technical Architecture

### Frontend (Mobile)
- **Framework**: React Native (Expo) or Flutter
- **QR Scanner**: expo-camera or qr_code package
- **State Management**: Redux or Context API
- **Styling**: TailwindCSS or built-in components

### Backend
- **Framework**: Node.js/Express or Python/Flask
- **Database**: Firebase (fastest) or PostgreSQL
- **Authentication**: Firebase Auth or JWT
- **Hosting**: Firebase Hosting (free tier sufficient)

### Admin Dashboard (Web)
- **Framework**: React or Vue
- **State Management**: Redux or Context API
- **Charts**: Chart.js or Recharts (data visualization)

---

## Questions by District (To Be Determined)
Analysis needed:
- Current greenery coverage per district
- Temperature differentials
- Air quality data
- Council roadmap priorities
- Resident demographics

**Output**: 1-3 tailored questions per district based on analysis

---

## Implementation Phases

### Phase 1 (Days 1-2): Setup & Data Analysis
- [ ] Scrape Madrid public data (geolocals, demographics, environment)
- [ ] Analyze data by district
- [ ] Generate district-specific questions

### Phase 2 (Days 2-3): MVP Development
- [ ] Build QR code mobile app (voting + comments)
- [ ] Build simple admin dashboard (view votes/comments)
- [ ] Setup database schema
- [ ] Deploy to Firebase

### Phase 3 (Days 3-4): Testing & Refinement
- [ ] QR code generation for each question
- [ ] Test voting flow end-to-end
- [ ] Populate initial questions
- [ ] UAT and bug fixes

### Phase 4 (Day 4-5): Launch Prep
- [ ] Deploy to production
- [ ] Generate QR codes for districts
- [ ] Print/post QR codes
- [ ] Documentation for council

---

## Success Metrics
- App deployed and accessible by end of week
- At least 1-2 questions live per district
- Ability to collect and view votes/comments
- Admin can see aggregated data across all districts

---

## Constraints
- **Timeline**: 4 days
- **Budget**: $0 (free tiers only)
- **Team**: 2 people
- **Platforms**: Mobile-first, web dashboard for admin

---

## Next Steps
1. Confirm tech stack preference
2. Begin data scraping/analysis phase
3. Define specific questions per district
4. Start development
