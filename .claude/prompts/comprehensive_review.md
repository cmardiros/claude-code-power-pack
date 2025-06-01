# Comprehensive Review Prompt Template

## Objective
Conduct a thorough, multi-layered validation of the provided plan using the QA specialist framework. This review should comprehensively assess objective achievement, quality standards, implementation viability, and identify risks and blind spots.

## QA Specialist Validation Framework

### 1. Objective Achievement Validation
- **Goal Alignment**: Does the plan clearly achieve stated objectives?
- **Success Criteria**: Are success metrics well-defined and measurable?
- **Scope Coverage**: Does the plan address all required functional areas?
- **Value Delivery**: Will this plan deliver meaningful business/technical value?

### 2. Quality Standards Assessment
- **Code Quality**: Are coding standards and best practices addressed?
- **Testing Strategy**: Is the testing approach comprehensive and appropriate?
- **Documentation**: Are documentation requirements adequate?
- **Maintainability**: Will the resulting system be maintainable long-term?
- **Performance**: Are performance considerations appropriately addressed?

### 3. Alternative Perspective Analysis
- **Architectural Alternatives**: Are other technical approaches considered?
- **Implementation Alternatives**: Could this be implemented differently?
- **Technology Choices**: Are technology selections well-justified?
- **Trade-off Analysis**: Are pros/cons of decisions clearly evaluated?

### 4. Implementation Viability Review
- **Resource Requirements**: Are time/skill/resource estimates realistic?
- **Technical Feasibility**: Are all technical approaches proven/viable?
- **Dependency Management**: Are external dependencies properly assessed?
- **Timeline Realism**: Is the proposed timeline achievable?
- **Risk Mitigation**: Are implementation risks identified and addressed?

### 5. Risk & Blind Spot Identification
- **Security Risks**: Are security implications thoroughly considered?
- **Scalability Risks**: Will this approach scale appropriately?
- **Operational Risks**: Are deployment/maintenance challenges addressed?
- **Integration Risks**: Are system integration challenges considered?
- **Business Continuity**: How does this affect ongoing operations?

## Comprehensive Assessment Areas

### Security Analysis
- **Authentication/Authorization**: Proper access controls
- **Data Protection**: Sensitive data handling
- **Input Validation**: Protection against malicious input
- **Communication Security**: Secure data transmission
- **Vulnerability Assessment**: Known security risks

### Feasibility Analysis
- **Technical Constraints**: Platform/technology limitations
- **Resource Constraints**: Team capacity and skills
- **Timeline Constraints**: Realistic delivery expectations
- **Budget Constraints**: Cost implications and efficiency
- **External Dependencies**: Third-party service reliability

### Maintainability Analysis
- **Code Structure**: Modular, readable, and extensible design
- **Documentation Quality**: Comprehensive technical documentation
- **Testing Coverage**: Unit, integration, and end-to-end testing
- **Monitoring/Observability**: Operational visibility and debugging
- **Update/Migration Strategy**: Future enhancement pathways

### Cost-Benefit Analysis
- **Development Costs**: Implementation time and resources
- **Operational Costs**: Ongoing maintenance and hosting
- **Opportunity Costs**: Alternative approaches not pursued
- **ROI Assessment**: Expected return on investment
- **Total Cost of Ownership**: Long-term cost implications

## Output Format

```markdown
# Comprehensive Review - [Plan Name]

## Executive Summary
**Overall Assessment**: [Critical Issues Found / Minor Issues Found / Plan Approved]
**Key Recommendation**: [Primary recommendation in 1-2 sentences]

## Quality Assessment Sections

### 1. Objective Achievement Validation
**Score**: [1-5] (1=Fails Objectives, 5=Exceeds Objectives)
- **Goal Alignment**: [Assessment with specific examples]
- **Success Criteria**: [Evaluation of measurability and clarity]
- **Scope Coverage**: [Analysis of completeness]
- **Value Delivery**: [Expected business/technical impact]
- **Issues Found**: [List specific objective-related concerns]

### 2. Quality Standards Assessment
**Score**: [1-5] (1=Poor Quality, 5=Excellent Quality)
- **Code Quality**: [Standards and best practices coverage]
- **Testing Strategy**: [Comprehensiveness and appropriateness]
- **Documentation**: [Adequacy for maintenance and onboarding]
- **Maintainability**: [Long-term sustainability assessment]
- **Performance**: [Performance considerations and optimization]
- **Issues Found**: [List specific quality concerns]

### 3. Alternative Perspective Analysis
**Score**: [1-5] (1=No Alternatives, 5=Well-Considered Alternatives)
- **Architectural Alternatives**: [Other technical approaches evaluated]
- **Implementation Alternatives**: [Different implementation paths]
- **Technology Choices**: [Justification for technology selections]
- **Trade-off Analysis**: [Explicit evaluation of pros/cons]
- **Issues Found**: [List perspective/alternative concerns]

### 4. Implementation Viability Review
**Score**: [1-5] (1=Not Viable, 5=Highly Viable)
- **Resource Requirements**: [Realism of estimates]
- **Technical Feasibility**: [Viability of technical approaches]
- **Dependency Management**: [External dependency assessment]
- **Timeline Realism**: [Achievability of proposed schedule]
- **Risk Mitigation**: [Implementation risk management]
- **Issues Found**: [List viability concerns]

### 5. Risk & Blind Spot Identification
**Score**: [1-5] (1=High Risk, 5=Well-Mitigated)
- **Security Risks**: [Security implications and protections]
- **Scalability Risks**: [Growth and performance challenges]
- **Operational Risks**: [Deployment and maintenance challenges]
- **Integration Risks**: [System integration complications]
- **Business Continuity**: [Impact on ongoing operations]
- **Issues Found**: [List specific risks and blind spots]

## Detailed Analysis

### Security Assessment
- **Critical Issues**: [High-priority security concerns]
- **Recommendations**: [Specific security improvements needed]
- **Compliance**: [Relevant security standards/regulations]

### Feasibility Assessment
- **Technical Constraints**: [Platform/technology limitations identified]
- **Resource Constraints**: [Team capacity and skill gaps]
- **External Dependencies**: [Third-party risks and alternatives]

### Maintainability Assessment
- **Code Structure**: [Design quality for long-term maintenance]
- **Documentation**: [Technical documentation completeness]
- **Testing Strategy**: [Coverage and quality of testing approach]
- **Monitoring**: [Operational visibility and debugging capabilities]

### Cost-Benefit Assessment
- **Development Investment**: [Time and resource requirements]
- **Operational Costs**: [Ongoing expenses and resource needs]
- **ROI Analysis**: [Expected return and value delivery timeline]
- **Alternatives**: [Cost comparison with alternative approaches]

## Critical Issues Summary
1. **Security Issues**: [List critical security gaps]
2. **Feasibility Issues**: [List critical feasibility concerns]
3. **Quality Issues**: [List critical quality problems]
4. **Risk Issues**: [List critical unmitigated risks]

## Recommendations by Priority

### High Priority (Must Address)
1. [Critical recommendation 1]
2. [Critical recommendation 2]
3. [Critical recommendation 3]

### Medium Priority (Should Address)
1. [Important recommendation 1]
2. [Important recommendation 2]
3. [Important recommendation 3]

### Low Priority (Nice to Address)
1. [Beneficial recommendation 1]
2. [Beneficial recommendation 2]
3. [Beneficial recommendation 3]

## Final Assessment
**Plan Status**: [Approved / Needs Minor Revision / Needs Major Revision / Rejected]
**Confidence Level**: [High / Medium / Low] confidence in assessment
**Key Strengths**: [Top 3 plan strengths]
**Key Weaknesses**: [Top 3 plan weaknesses]
**Next Steps**: [Recommended immediate actions]
```

## Quality Indicators

A high-quality comprehensive review should:
- Systematically evaluate all five framework areas
- Provide specific, actionable recommendations
- Identify both obvious and subtle issues
- Consider long-term implications and consequences
- Balance thoroughness with practical constraints
- Include concrete examples and evidence
- Prioritize issues by business impact
- Offer constructive alternatives for identified problems