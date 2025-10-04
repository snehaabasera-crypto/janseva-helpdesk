JanSeva HelpDesk - Rural Survey & FAQ Assistant
A multilingual AI assistant built on Inya.ai for rural communities, providing consent-based surveys and verifiable government information across Voice, Chat, and SMS channels.

🚀 Quick Setup
Prerequisites
Inya.ai account with Custom Integrations enabled

Vercel account for serverless API deployment

GitHub account for code repository

Environment Variables
No environment variables required - all APIs are public GET endpoints with query parameters.

📋 Setup Instructions
Part A: Deploy Backend APIs (Vercel)
Clone Repository

bash
git clone [your-repo-url]
cd janseva-helpdesk
Deploy to Vercel

bash
npm install -g vercel
vercel login
vercel --prod
Verify API Endpoints
Test these URLs in browser (replace YOUR-DOMAIN):

PMAY API: https://YOUR-DOMAIN.vercel.app/api/pmay?domain=pmay&query_type=eligibility

Pincode API: https://YOUR-DOMAIN.vercel.app/api/pincode?pincode=110001

MP API: https://YOUR-DOMAIN.vercel.app/api/mp?pincode=110001

Part B: Configure Inya.ai Integrations
Create Three Custom Integrations

Login to Inya.ai → Integrations → Add Custom Integration

Create separate integrations for each API:

PMAY Mock API: https://YOUR-DOMAIN.vercel.app/api/pmay

Pincode Mock API: https://YOUR-DOMAIN.vercel.app/api/pincode

MP Mock API: https://YOUR-DOMAIN.vercel.app/api/mp

Create Actions for Each Integration

PMAY Actions:

Action: pmay_query

URL: ?domain=pmay&query_type={scheme_query}&mock=true

Variables: scheme_query (String)

Pincode Actions:

Action: pincode_lookup

URL: ?pincode={pincode}&mock=true

Variables: pincode (String)

Action: pincode_directory

URL: ?state={state}&district={district}&limit={limit}&mock=true

Variables: state, district, limit (all String)

MP Actions:

Action: mp_by_pincode

URL: ?pincode={pincode}&mock=true

Variables: pincode (String)

Action: mp_by_constituency

URL: ?constituency={constituency}&mock=true

Variables: constituency (String)

Configure Pre-call Variables

text
user_pincode: 110001
preferred_language: hi
channel: voice
consent_status: granted
audit_enabled: true
source_label: Mock Rural APIs (Vercel)
🧪 Testing Instructions
API Testing
Test Each Endpoint Individually

bash
# PMAY Test
curl "https://YOUR-DOMAIN.vercel.app/api/pmay?domain=pmay&query_type=eligibility"

# Pincode Test
curl "https://YOUR-DOMAIN.vercel.app/api/pincode?pincode=110001"

# MP Test
curl "https://YOUR-DOMAIN.vercel.app/api/mp?pincode=110001"
Verify JSON Response Format

Each should return valid JSON

Check for disclaimer field in responses

Confirm 200 OK status

Inya.ai Action Testing
Test Each Action

Go to Integrations → Actions → Select Action

Click "Test API Request"

Enter test values:

pincode: 110001

scheme_query: eligibility

constituency: Lucknow

state: maharashtra, limit: 10

Verify Action Logs

Check Action Logs for successful calls

Confirm response time < 5 seconds

Validate JSON structure matches expectations

End-to-End Conversation Testing
Test Scenarios:

PMAY Eligibility Query

Input: "PMAY ke liye eligible hun?"

Expected: Calls pmay_query action, returns eligibility criteria

Pincode Lookup

Input: "110001 ke bare mein batao"

Expected: Calls pincode_lookup, returns location details

MP Information

Input: "Mere MP kaun hain? Pincode 110001"

Expected: Calls mp_by_pincode, returns MP details

Survey Flow

Input: "Survey dena chahta hun"

Expected: Asks consent, collects MLA/MP feedback

Language Switch

Input: "English mein baat karte hain"

Expected: Switches language, maintains context

Rural Communication Testing
Test these specific phrases to verify cultural sensitivity:

"Aaj tomato ka bhav kya hai?" (Price inquiry)

"Nearest aanganwadi kahan hai?" (Local service location)

"MLA Sharma ji hain" (Name confirmation flow)

"Survey dena chahta hun" (Consent workflow)

Error Testing
Network Failures

Temporarily disable one API endpoint

Verify fallback behavior and "approximate data" labeling

Invalid Inputs

Test with invalid pincode: "000000"

Test with non-existent constituency: "XYZConstituency"

🔍 Troubleshooting
Common Issues:

404 on API endpoints

Check Vercel deployment status

Verify file paths: /api/pmay.js, /api/pincode.js, /api/mp.js

Inya.ai Actions not working

Verify Integration URLs are correct

Check Action variable names match URL template

Ensure no extra variables defined

Empty responses

Check query parameter format

Verify mock data is properly loaded

Test endpoint directly in browser

📊 Performance Metrics
API Response Time: < 2 seconds

Action Success Rate: > 95%

Conversation Completion: > 90%

🎯 Key Features Demonstrated
Multilingual Support: Hindi, English, regional languages

Channel-Native Responses: Voice (brief), Chat (detailed), SMS (compact)

Consent-First Surveys: Explicit permission before storing opinions

Fallback Resilience: Live → Cache → Mock with transparency

Rural UX: Polite forms, local terminology, confirmation flows

Political Neutrality: Declines voting advice, maintains strict impartiality

🤝 Support
For issues or questions:

Check Action Logs in Inya.ai

Test APIs directly via browser

Verify pre-call variables are set correctly

📝 License
MIT License - See LICENSE file for details
