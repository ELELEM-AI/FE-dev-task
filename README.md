# Frontend Developer — Skills Assessment

Welcome to the elelem Frontend Developer assessment.  
This task is designed to simulate real work at elelem: improving code quality, fixing issues, building features, and working with real API contracts.

Clone this GitHub repository containing a React application to get started.
Your goal is to complete all required deliverables within **48 hours** after receiving the repository link.

> [!IMPORTANT]
> - This repo is archived
> - You should fork the repository
> - Go to settings and make the repo private
> - Create the PR and issues in your own forked repo
> - Once you are done, invite @SheikSadi to review your work

> [!CAUTION]
> - Do NOT keep your repo public and make sure no one can plagiarize.

---

## 🚀 Deliverables Overview

### **1. Bug Identification & Reporting**
Perform stress testing and exploratory testing across all flows.

**Deliverable:**  
A complete **Error Report** using the required format (see below).

---

### **2. Functionality Completion**
Make the application fully functional, covering all functional and non-functional requirements.

**Deliverable:**  
A **Pull Request (PR)** with all working changes, including code fixes, integrations, enhancements, and refactors where needed.

---

### **3. Improvements & Suggestions**
Review the overall codebase and propose meaningful improvements.

**Deliverable:**  
A set of **GitHub Issues** describing each improvement (UX, code quality, architecture, optimization, DX, etc.)

---

### **4. (Optional but Highly Recommended)** Automated UI Tests
Showcase engineering maturity by adding minimal automated UI tests (Cypress / Playwright / React Testing Library).

---

## 🐞 Error Report Format

Please document each bug using the following structure:

| Bug Summary | Steps to Reproduce | Expected Result | Evidence |
|-------------|--------------------|-----------------|----------|
| Page remains stuck on “Verifying…” when the user enters an incorrect OTP code | 1. Navigate to root URL <br>2. Fill required fields (Website, Country, About optional, CSV optional, Email, First name, Last name, Password) <br>3. Click "Continue" <br>4. Enter an incorrect OTP in the verification modal <br>5. Click "Verify code" | Loader should stop and show: “Invalid OTP. Please try again.” User should be able to retry without a refresh. | https://somup.com/cTXti9RIeH |
| Describe the bug | Steps to reproduce | Describe expected behaviour | Screen recording link |
| ... | ... | ... | ... |

---

## 🔌 Backend API Contract

These are the API endpoints your frontend must integrate with:

| Method | Endpoint | Query Params | Headers | Body | 200 Response | Requires Cookie | Sets Cookie |
|--------|----------|--------------|---------|------|--------------|----------------|--------------|
| GET | `/api/v1/session/start` | - | `Content-Type: application/json` | _ | `{ onboardingId }` | - | `session_token` |
| POST | `/api/v1/user-verification/send-otp` | onboardingId | `Content-Type: application/json` | `{ email }` | `{ success, message }` | session_token | - |
| POST | `/api/v1/user-verification/verify-otp` | onboardingId | `Content-Type: application/json` | `{ email, otp }` | `{ success, message }` | session_token | `auth_token` |
| PUT | `/api/v1/business-logic/csv-upload` | onboardingId | `Content-Type: multipart/form-data` | CSV file | `{ success, message }` | session_token, auth_token | - |
| POST | `/api/v1/business-logic/get-started` | onboardingId | `Content-Type: application/json` | `GetStartedRequest` | `BusinessLogic` | session_token, auth_token | - |
| POST | `/api/v1/business-logic/confirm` | onboardingId | `Content-Type: application/json` | `BusinessLogic` | `{ success, message }` | session_token, auth_token | - |
| PUT | `/api/v1/complete-onboarding` | onboardingId | `Content-Type: application/json` | onboardingId | `{ success, message }` | session_token, auth_token | - |

---

## 📦 Schema Definitions (Pydantic)

### **GetStartedRequest**
```py
class UserInfo(BaseModel):
    email: str
    firstname: str
    lastname: str
    password: str

class ClientInfo(BaseModel):
    website: str
    country: str
    about: Optional[str]

class GetStartedRequest(BaseModel):
    user: UserInfo
    client: ClientInfo
```

### **BusinessLogic**

```py
class Brand(BaseModel):
    name: str
    domain: str
    brand_name_variations: List[str] = []

class BusinessLogic(BaseModel):
    own_brand: Brand
    competitor_brands: List[Brand]
```

---

## 📝 Submission Guidelines

Your final submission must include:

* ✔ **Error Report**
* ✔ **Pull Request** with functional fixes
* ✔ **GitHub Issues** for improvements
* ✔ (Optional) **Automated UI tests**

Please ensure your PR and issues are clear, descriptive, and professional.

---

If you need clarifications, reach out anytime at sheik.sadi@elelem.ai. Good luck — we’re excited to see your work!
