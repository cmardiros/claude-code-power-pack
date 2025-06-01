# Simplicity Review Prompt Template

## Objective
Evaluate the provided plan for clarity, complexity reduction, and simplification opportunities. Focus on identifying over-engineering, unnecessary complexity, and areas where the plan can be streamlined without losing core value.

## Review Framework

### 1. Clarity Assessment
- **Communication Clarity**: Is the plan easily understood by implementers?
- **Objective Clarity**: Are the goals and success criteria clearly defined?
- **Step Clarity**: Are implementation steps concrete and actionable?

### 2. Complexity Analysis
- **Architectural Complexity**: Are there simpler architectural approaches?
- **Implementation Complexity**: Can implementation steps be simplified?
- **Dependency Complexity**: Are all dependencies necessary?
- **Operational Complexity**: Will this be easy to maintain and operate?

### 3. Over-Engineering Detection
- **Feature Scope**: Are all proposed features essential for the core objective?
- **Technical Scope**: Is the technical approach proportional to the problem?
- **Future-Proofing**: Is the plan over-engineered for theoretical future needs?

### 4. Minimum Viable Approach
- **Core Value Identification**: What's the smallest version that delivers value?
- **Phased Implementation**: Can this be broken into simpler phases?
- **Essential vs Nice-to-Have**: Which components are truly necessary?

## Key Evaluation Questions

1. **Can this plan be simplified without losing core value?**
   - Identify specific areas of unnecessary complexity
   - Propose simpler alternatives that achieve the same goals

2. **Are there unnecessary complexities or over-engineering?**
   - Flag architectural decisions that seem disproportionate
   - Identify features that may be premature optimization

3. **Is the plan clear and easy to understand for implementers?**
   - Assess if technical decisions are well-justified
   - Check if implementation steps are concrete and actionable

4. **What's the minimum viable version of this plan?**
   - Define the smallest implementation that delivers value
   - Suggest a phased approach if the current plan is too ambitious

## Output Format

```markdown
# Simplicity Review - [Plan Name]

## Executive Summary
[2-3 sentences summarizing the simplicity assessment]

## Clarity Assessment
**Score**: [1-5] (1=Very Unclear, 5=Very Clear)
- **Strengths**: [List clear aspects]
- **Issues**: [List unclear or confusing elements]
- **Recommendations**: [Specific suggestions for improvement]

## Complexity Analysis
**Score**: [1-5] (1=Overly Complex, 5=Appropriately Simple)
- **Architectural Complexity**: [Assessment with examples]
- **Implementation Complexity**: [Assessment with examples]
- **Operational Complexity**: [Assessment with examples]

## Over-Engineering Indicators
- **Identified Issues**: [List specific over-engineering concerns]
- **Unnecessary Features**: [Features that could be removed/simplified]
- **Disproportionate Solutions**: [Technical approaches that seem excessive]

## Minimum Viable Alternative
**Proposed MVP**: [Description of simpler approach]
- **Core Components**: [Essential elements only]
- **Removed Complexity**: [What can be eliminated]
- **Phased Approach**: [How to implement incrementally]

## Simplification Recommendations
1. **High Priority**: [Critical simplifications]
2. **Medium Priority**: [Beneficial simplifications]
3. **Low Priority**: [Optional simplifications]

## Risk Assessment
- **Simplification Risks**: [What could go wrong with simpler approach]
- **Complexity Risks**: [What could go wrong with current approach]
- **Mitigation Strategies**: [How to address identified risks]

## Final Recommendation
**Overall Assessment**: [Keep as-is / Minor simplification needed / Major simplification needed]
**Key Actions**: [Top 3 specific actions to improve simplicity]
```

## Examples of Simplicity Improvements

### Good Simplicity Practices
- **Single Responsibility**: Each component has one clear purpose
- **Incremental Implementation**: Complex features built in phases
- **Standard Solutions**: Using existing libraries instead of custom implementations
- **Clear Dependencies**: Minimal, well-justified external dependencies

### Common Complexity Anti-Patterns
- **Premature Optimization**: Building for scale before it's needed
- **Feature Creep**: Adding nice-to-have features to the core plan
- **Custom Everything**: Building custom solutions for standard problems
- **Monolithic Phases**: Trying to implement everything at once

### Simplification Strategies
- **Phase Splitting**: Break large features into smaller, valuable increments
- **Standard Libraries**: Replace custom implementations with proven solutions
- **Scope Reduction**: Focus on core value proposition
- **Dependency Minimization**: Remove or replace complex dependencies

## Quality Indicators

A high-quality simplicity review should:
- Identify specific complexity issues with concrete examples
- Propose actionable simplification strategies
- Maintain focus on delivering core value
- Consider both implementation and operational simplicity
- Balance simplicity with necessary functionality
- Provide clear, prioritized recommendations