
# 🇩🇿 7aniwlou (حنيولو) - Platform Reporting for Algeria

> **"Catch the crime, fix the street — together."**

7aniwlou is a community-driven reporting platform designed specifically for Algerian citizens to anonymously report crimes, hazards, and public infrastructure issues. Built with Arabic-first design and real understanding of Algerian urban challenges.

![Arabic RTL](https://img.shields.io/badge/Arabic-RTL%20Support-green)
![React](https://img.shields.io/badge/React-18.3.1-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)
![Supabase](https://img.shields.io/badge/Supabase-Ready-green)

## 🌟 Key Features

- **🔍 Anonymous Reporting**: Submit reports without registration required
- **📱 Mobile-First Design**: Fully responsive Arabic interface (RTL)
- **🗺️ Interactive Maps**: Geographic view of community reports
- **📊 Real-time Dashboard**: Track community statistics and trends
- **🚨 Emergency Integration**: Direct access to police (17/1548) and emergency (14/1021)
- **🎯 Smart Filtering**: Filter by category, wilaya, status, and popularity
- **❤️ Community Engagement**: Like and interact with reports
- **🔐 Privacy-First**: Built-in privacy protection and data anonymization

## 🛠️ Tech Stack

- **Frontend**: React 18 + TypeScript + Vite
- **Styling**: TailwindCSS with custom Arabic design system
- **Backend**: Supabase (PostgreSQL + Auth + Storage)
- **State Management**: TanStack React Query v5
- **UI Components**: Custom shadcn/ui implementation
- **Icons**: Lucide React
- **Routing**: React Router DOM v6

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Supabase account

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/7aniwlou.git
cd 7aniwlou

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Add your Supabase credentials

# Start development server
npm run dev
```

### Environment Variables

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

## 📁 Project Structure

```
src/
├── components/          # Reusable UI components
├── pages/              # Route components
├── hooks/              # Custom React hooks
├── integrations/       # Supabase client and types
├── data/               # Mock data and constants
└── lib/                # Utility functions

project-docs/           # Comprehensive documentation
├── overview.md         # Project overview and features
├── plan.md             # Strategic execution plan
├── sprints.md          # Development roadmap
└── ...                 # Additional technical docs
```

## 🇩🇿 Contributing (للمطورين الجزائريين)

We welcome contributions from Algerian developers who understand local needs and challenges!

### Why Contribute?

- 🎯 **Impact**: Help build something that matters for Algerian communities
- 🧠 **Learn**: Work with modern React, TypeScript, and Supabase
- 🤝 **Network**: Connect with other Algerian developers
- 🔧 **Skills**: Gain experience with real-world production apps

### How to Contribute

1. **Fork the repository**
2. **Check `/project-docs/sprints.md`** for current development priorities
3. **Pick a sprint task** that matches your skills
4. **Create a feature branch**: `git checkout -b feature/your-feature-name`
5. **Make your changes** following our coding standards
6. **Test thoroughly** on both desktop and mobile
7. **Submit a Pull Request** with detailed description

### Development Priorities (Current Sprint)

Check `/project-docs/sprints.md` for the latest development roadmap. We're currently focusing on:

- 🔐 **Authentication System**: Supabase integration
- 📊 **Database Schema**: Reports and user management
- 🎨 **UI/UX Polish**: Mobile responsiveness and Arabic RTL
- 🔍 **Real Data Integration**: Moving from mock to live data

### Contribution Guidelines

- **Arabic-First**: All UI text should be in Arabic with proper RTL support
- **Mobile-Responsive**: Test on various screen sizes
- **Clean Code**: Follow TypeScript best practices
- **Documentation**: Update docs when adding features
- **Testing**: Ensure features work end-to-end

### Local Development Tips

```bash
# Run with Arabic RTL testing
npm run dev

# Type checking
npm run type-check

# Build for production
npm run build

# Preview production build
npm run preview
```

## 📋 Current Status & Roadmap

### ✅ Completed
- Fully responsive Arabic UI with RTL support
- Complete component library and design system
- Multi-step report submission form
- Interactive map integration
- Dashboard with statistics
- Authentication UI (username/password)

### 🚧 In Progress (See `/project-docs/sprints.md`)
- Supabase backend integration
- Real authentication system
- Database schema and RLS policies
- File upload for photos/videos
- Real-time data synchronization

### 🎯 Upcoming
- Advanced filtering and search
- Admin moderation tools
- Performance optimization
- Progressive Web App features

## 🔒 Security & Privacy

7aniwlou is built with privacy and security as core principles:

- **Anonymous Reporting**: No personal data required
- **Data Protection**: Row Level Security (RLS) policies
- **File Validation**: Secure file upload with type checking
- **Rate Limiting**: Protection against spam and abuse
- **Privacy Guidelines**: Built-in recommendations for photo/video privacy

## 📚 Documentation

Comprehensive documentation is available in `/project-docs/`:

- **[Overview](project-docs/overview.md)**: Project goals and features
- **[Development Plan](project-docs/plan.md)**: Strategic execution roadmap
- **[Sprint Guide](project-docs/sprints.md)**: Week-by-week development tasks
- **[Architecture](project-docs/data-integrations.md)**: Technical implementation details

## 🔒 Security Review Summary

The following section is an in-repo copy of `project-docs/security-review-summary.md` for ease of discovery on GitHub. Source of truth remains the file in `project-docs/`.

### 🚨 CRITICAL SECURITY ISSUES

1. Complete Lack of Backend Security Foundation
- No Database Tables: The Supabase database is completely empty with no tables, RLS policies, or proper data structure
- Mock Authentication Only: Authentication is entirely client-side using `localStorage` with no real backend validation
- No Data Persistence: All reports are mock data with no real database integration
- Impact: This is a MAJOR SECURITY GAP - anyone can manipulate client-side data, and there's no actual security protection

2. Insecure Authentication Implementation
- Client-Side Only: Authentication uses only `localStorage.setItem("user", JSON.stringify({username}))`
- No Password Hashing: Passwords aren't validated against any backend system
- No Session Management: No proper session tokens, JWT, or secure authentication flow
- Weak Password Requirements: Only requires 6 characters minimum
- Impact: CRITICAL - Anyone can bypass authentication by manipulating localStorage

3. Input Validation & XSS Vulnerabilities
- No Input Sanitization: Form inputs (title, description, location) have no validation or sanitization
- Direct Display: User content is rendered directly without sanitization (potential XSS)
- No File Upload Security: Media upload functionality is not implemented but planned without security considerations
- Impact: HIGH - Potential for Cross-Site Scripting attacks and malicious content injection

### ⚠️ SIGNIFICANT SECURITY CONCERNS

4. Data Exposure Risks
- No Access Controls: When database is implemented, there are no RLS policies to restrict data access
- Public Data by Default: Reports would be accessible to anyone without proper authorization
- No Data Anonymization: Despite claims of anonymity, no mechanisms ensure user privacy

5. Supabase Configuration Issues
- Function Security: Database functions don't have proper `search_path` security settings
- OTP Configuration: Authentication OTP expiry settings exceed recommended thresholds
- No Row Level Security: Database has no RLS policies implemented

### 📋 MINOR SECURITY IMPROVEMENTS NEEDED

6. Frontend Security Headers (when deployed)
- Missing security headers (CSP, HSTS, etc.)
- No protection against clickjacking
- Note: The exposed Supabase URL and anon key in client code are intentionally public per Supabase architecture

7. Development Security
- Using `setTimeout` in authentication flow (acceptable for mock data)
- Single `dangerouslySetInnerHTML` usage in chart component (controlled, low risk)

## 🔥 IMMEDIATE SECURITY ACTION REQUIRED

The application currently has NO REAL SECURITY - it's entirely a frontend demo with mock data. Before any production use, critical backend security infrastructure must be implemented.

### Critical Security Implementation Plan

#### Phase 1: Database Foundation & Authentication (Week 1-2)
1. Create Secure Database Schema
   - Create `profiles` table with proper RLS policies
   - Create `reports` table with comprehensive RLS policies
   - Create `report_likes` and `report_views` tables
   - Implement role-based access control with `user_roles` table

2. Implement Real Authentication
   - Replace mock authentication with Supabase Auth
   - Implement proper signup/login flows with email/password
   - Add session management and token handling
   - Implement protected routes and authentication guards
   - Add proper logout functionality

3. Row Level Security (RLS) Implementation
   - Enable RLS on all tables
   - Create policies for user data access (users can only see their own profiles)
   - Create policies for reports (anonymous reports visible to all, user reports controlled by owner)
   - Implement admin access policies if needed

#### Phase 2: Input Validation & Data Protection (Week 2-3)
4. Frontend Input Validation & Sanitization
   - Add comprehensive form validation using Zod schemas
   - Implement client-side input sanitization
   - Add XSS protection for user-generated content
   - Validate all form inputs before submission

5. Backend Validation & Security
   - Create Supabase Edge Functions for server-side validation
   - Implement proper error handling without information leakage
   - Add rate limiting for report submissions
   - Validate file uploads and implement virus scanning

6. Database Security Hardening
   - Fix function search_path security issues
   - Configure proper OTP expiry settings
   - Add database triggers for data validation
   - Implement audit logging for sensitive operations

#### Phase 3: Advanced Security Features (Week 3-4)
7. File Upload Security
   - Implement secure file upload to Supabase Storage
   - Add file type validation and size limits
   - Implement automatic face/license plate blurring
   - Add malware scanning for uploaded files

8. Privacy & Anonymity Protection
   - Implement true anonymous reporting (no user tracking)
   - Add IP anonymization for anonymous reports
   - Implement data retention policies
   - Add user data deletion capabilities

9. Security Monitoring & Logging
   - Add security event logging
   - Implement failed authentication attempt monitoring
   - Add suspicious activity detection
   - Create security dashboard for administrators

#### Phase 4: Production Security (Week 4)
10. Production Hardening
    - Configure security headers (CSP, HSTS, etc.)
    - Set up proper error handling and logging
    - Implement backup and disaster recovery
    - Add security testing and penetration testing
    - Configure monitoring and alerting

11. Compliance & Legal
    - Ensure GDPR compliance for user data
    - Implement data subject rights (access, deletion)
    - Add proper terms of service and privacy policy
    - Configure data retention and deletion policies

> Source: `project-docs/security-review-summary.md`

## 🤝 Community & Support

### For Developers
- **GitHub Issues**: Bug reports and feature requests
- **Discussions**: Technical questions and ideas
- **Pull Requests**: Code contributions welcome

### For Users
- **Feature Requests**: Share ideas for improving the platform
- **Bug Reports**: Help us identify and fix issues
- **Community Feedback**: Tell us how we can better serve Algerian communities

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built for the Algerian community with love and dedication
- Inspired by the need for transparent, community-driven reporting
- Thanks to all contributors who help make this platform better

---

**Ready to contribute?** Start by reading `/project-docs/sprints.md` and pick a task that interests you!

**مستعد للمساهمة؟** ابدأ بقراءة دليل التطوير واختر مهمة تهمك!
