# Talk & Comment - QA Trial Test Plan

> **Goal:** Discover the "unknown unknowns"—what breaks that current integration tests don't catch
> 
> **Focus:** Full user journey validation, cross-platform compatibility, and silent failure detection
> 
> **Duration:** 3-4 weeks (starts after v3.3 ships)

---

## Table of Contents

- [The Idea: Integration Resilience Testing](#the-idea-integration-resilience-testing)
- [Trial Structure](#trial-structure)
- [Testing Focus Areas](#testing-focus-areas)
- [Stack & Tools](#stack--tools)
- [Cost Options](#cost-options)
- [What You Get](#what-you-get)
- [What I Need From You](#what-i-need-from-you)

---

## The Idea: Integration Resilience Testing

### What's Different From Current Testing

You already have unit tests (Jest/RSpec) and e2e tests (Playwright) for individual components. This focuses on what those miss:

- **Real user journey edge cases** - What happens when users do unexpected things
- **Cross-platform compatibility** - Does it actually work everywhere users share links
- **Silent failures** - Issues that don't throw errors but degrade experience
- **Browser update resilience** - Testing across Chrome versions and OS combinations
- **Unknown unknowns** - Problems you haven't thought about yet

### Core Testing Strategy

Instead of comprehensive test coverage, focus on **strategic validation** of critical integration points across the full stack:

```
Chrome Extension → Rails Backend → Worker Services → User Platforms
```

---

## Trial Structure

###  Week 1: Discovery & Profiling

**Objective:** Understand what breaks that current tests don't catch

**Activities:**
- Audit existing integration test coverage
- Profile complete user journey (install → record → share → link validation)
- Test across realistic teacher scenarios (classroom wifi, multiple tabs, quick feedback)
- Map risk areas and integration failure points
- Test cross-platform compatibility (LMS systems, comment sections, social platforms)

**Deliverables:**
- Document of "it breaks here" scenarios
- Risk map of integration points
- Gap analysis of current test coverage

**Tools Used:**
- Manual testing across platforms
- Chrome DevTools for extension debugging
- Network analysis for API calls

---

### Week 2-3: Build Monitoring & Automation

**Objective:** Set up infrastructure to catch silent failures and unknown issues

#### Observability Setup
- Implement OpenTelemetry + Tempo for distributed tracing (extension → backend → workers)
- Set up Sentry or GlitchTip for client-side error tracking
- Create Grafana dashboards for quality metrics alongside existing performance metrics

#### Automated Testing
- Extend Playwright tests for discovered edge cases
- Add full-system validation tests (install → record → transcribe → share → verify)
- Test platform-specific link compatibility
- Validate browser update resilience

#### Monitoring
- External monitoring setup (Checkly or similar) for "does it work from real user locations"
- Alerts for integration failures before users report them

**Deliverables:**
- Working observability infrastructure
- Extended test suite for critical gaps
- Automated monitoring with alerts
- Quality metrics dashboards

**Tools Used:**
- OpenTelemetry + Tempo (distributed tracing)
- Sentry/GlitchTip (error tracking)
- Grafana (quality dashboards)
- Playwright (extended e2e tests)
- Checkly or Uptime Kuma (external monitoring)

---

### Week 4: Validation & Documentation

**Objective:** Validate infrastructure works and create ongoing testing strategy

**Activities:**
- Run full test suite, validate monitoring catches real issues
- Document discovered "unknown unknowns" with recommendations
- Create runbook for ongoing testing strategy
- Knowledge transfer session

**Deliverables:**
- Final report of findings and recommendations
- Ongoing testing strategy documentation
- Monitoring dashboards with baseline metrics
- Runbook for maintaining test infrastructure

---

## Testing Focus Areas

### 1. User Journey Edge Cases

**What to test:**
- Recording interrupted mid-session
- Poor internet during transcription
- Multiple simultaneous recordings
- Extension updates while in use
- Offline mode behavior

**Why it matters:** Users don't follow happy paths—they multitask, lose connection, update browsers at inconvenient times

---

### 2. Cross-Platform Link Sharing

**What to test:**

Does shared link render correctly in:
- LMS platforms (Canvas, Moodle, Blackboard)
- Google Classroom
- Social media comment sections
- Email clients
- Mobile browsers
- Link formatting in different contexts
- Playback experience for recipients

**Why it matters:** A link that works in testing but breaks in specific platforms kills user trust

---

### 3. Browser & OS Compatibility

**What to test:**
- Different Chrome versions
- Chrome on Windows vs Mac vs Linux
- Permissions handling across OS
- Extension behavior after Chrome updates
- Microphone access across different setups

**Why it matters:** Your "it works in my environment" doesn't match user reality

---

### 4. Worker & Backend Integration

**What to test:**
- Worker behavior under load
- Race conditions in distributed system
- What happens when workers fail silently
- API failures and retry logic
- Link generation reliability

**Why it matters:** Backend issues often don't surface in frontend tests but break user experience

---

## Stack & Tools

### What You Already Have
```
✓ Jest/RSpec (unit tests)
✓ Playwright (e2e tests)
✓ Prometheus/Grafana/Loki (observability)
✓ Rails backend
✓ Worker services
```

### What Gets Added
- **OpenTelemetry + Tempo** - Distributed tracing across full stack
- **Sentry/GlitchTip** - Error tracking for silent failures
- **Extended Playwright tests** - Full system e2e validation
- **Checkly or Uptime Kuma** - External monitoring from real locations
- **Custom Grafana dashboards** - Quality metrics visualization

### Why These Tools
All integrate with your existing Prometheus/Grafana/Loki stack. Most are open-source. Focus on observability over exhaustive testing.

---

## Cost Options

Choose what works best:

### Option A: Weekly Rate
**$200/week for 4 weeks** 
- Flexible if scope changes
- Adjust timeline if needed
- Pay weekly as work progresses
- (recommended for simplicity)

### Option B: Hourly (Capped)
**$13/hour, max 60 hours** 
- Pay for actual time
- Track time transparently
- Cap provides budget certainty

---

## What You Get

### Immediate
- Discovered issues you didn't know existed
- Working monitoring infrastructure
- Automated tests for critical gaps
- Peace of mind about integration resilience

### Ongoing
- Quality metrics visible in your existing Grafana
- Alerts when integration breaks
- Testing strategy for future updates
- Knowledge of where system is fragile

---

## What I Need From You

### Access
- Codebase (read access minimum, write access helpful)
- Staging environment
- Error logs and user feedback data
- Usage patterns (where users actually share links)

### Context
- 30-60 min kickoff call
- Quick questions as I discover issues
- Final knowledge transfer session

### Flexibility
- Some approaches will work immediately, others need iteration
- This is co-building, not just executing

---

## Start Date

**After v3.3 ships** - You focus on shipping, I'll be ready when you are


---

## Questions?

Happy to adjust scope, timeline, or approach based on what makes sense for Talk & Comment.

---

**Document prepared by:** Meriem  
**Date:** October 20, 2025  
**Version:** 1.0
