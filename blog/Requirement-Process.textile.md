A well-formed requirement is a statement that 
 can be verified, 
 has to be met or possessed by a system to solve a stakeholder problem or to achieve a stakeholder 
objective, 
 is qualified by measurable conditions and bounded by constraints, and 
 defines the performance of the system when used by a specific stakeholder or the corresponding 
capability of the system, but not a capability of the user, operator, or other stakeholder.

 Requirements are mandatory binding provisions and use 'shall'. 
 Statements of fact, futurity, or a declaration of purpose are non-mandatory, non-binding provisions and use 'will'. 'Will' can also be used to establish context or limitations of use. However, 'will' can be construed as legally binding, so it is best to avoid using it for requirements. 
 Preferences or goals are desired, non-mandatory, non-binding provisions and use 'should'. 
 Suggestions or allowances are non-mandatory, non-binding provisions and use 'may'. 
 Non-requirements, such as descriptive text, use verbs such as ‘are', ‘is', and ‘was'. It is best to avoid 
using the term ‘must', due to potential misinterpretation as a requirement. 
 Use positive statements and avoid negative requirements such as ‘shall not'. 
 Use active voice: avoid using passive voice, such as 'shall be able to select'. 

Examples of constraints include: 
 interfaces to already existing systems (e.g., format, protocol, or content) where the interface cannot be 
changed, 
 physical size limitations (e.g., a controller shall fit within a limited space in an airplane wing), 
 laws of a particular country, 
 available duration or budget, 
 pre-existing technology platform, 
 user or operator capabilities and limitations.

Each stakeholder, system, and system element requirement shall possess the following characteristics: 
 Necessary. The requirement defines an essential capability, characteristic, constraint, and/or quality 
factor. If it is removed or deleted, a deficiency will exist, which cannot be fulfilled by other capabilities of 
the product or process. The requirement is currently applicable and has not been made obsolete by the 
passage of time. Requirements with planned expiration dates or applicability dates are clearly identified. 
Implementation Free. The requirement, while addressing what is necessary and sufficient in the system, 
avoids placing unnecessary constraints on the architectural design. The objective is to be implementationindependent. The requirement states what is required, not how the requirement should be met. 
NOTE  While such information may still be important, the information should be documented and communicated in 
some other form of documentation, such as the requirements attributes in subclause 5.2.8 (e.g., rationale) in order to aid in 
design and implementation. Additionally, including design solutions in the requirements may risk the possibility that 
potential design solutions may be overlooked or eliminated. Examples include stating requirements that express an exact 
commercial system set or a system that can be bought rather than made, stating tolerances for items deep within the 
conceptual system, or establishing constraints that are not necessarily reflective of the parent requirement. 
Unambiguous. The requirement is stated in such a way so that it can be interpreted in only one way. The 
requirement is stated simply and is easy to understand. 
Consistent. The requirement is free of conflicts with other requirements.
Complete. The stated requirement needs no further amplification because it is measurable and sufficiently 
describes the capability and characteristics to meet the stakeholder's need. 
 Singular. The requirement statement includes only one requirement with no use of conjunctions. 
 Feasible. The requirement is technically achievable, does not require major technology advances, and fits 
within system constraints (e.g., cost, schedule, technical, legal, regulatory) with acceptable risk. 
Traceable. The requirement is upwards traceable to specific documented stakeholder statement(s) of 
need, higher tier requirement, or other source (e.g., a trade or design study). The requirement is also 
downwards traceable to the specific requirements in the lower tier requirements specification or other 
system definition artefacts. That is, all parent-child relationships for the requirement are identified in 
tracing such that the requirement traces to its source and implementation. 
Verifiable. The requirement has the means to prove that the system satisfies the specified requirement. 
Evidence may be collected that proves that the system can satisfy the specified requirement. Verifiability 
is enhanced when the requirement is measurable.

Vague and general terms shall be avoided. They result in requirements that are often difficult or even 
impossible to verify or may allow for multiple interpretations.  The following are types of unbounded or ambiguous terms: 
 Superlatives (such as 'best', 'most') 
 Subjective language (such as 'user friendly', 'easy to use', 'cost effective') 
 Vague pronouns (such as 'it', 'this', 'that') 
 Ambiguous adverbs and adjectives (such as 'almost always', 'significant', 'minimal') 
 Open-ended, non-verifiable terms (such as 'provide support', 'but not limited to', 'as a minimum') 
 Comparative phrases (such as 'better than', 'higher quality') 
 Loopholes (such as 'if possible', 'as appropriate', 'as applicable') 
 Incomplete references (not specifying the reference with its date and version number; not specifying just 
the applicable parts of the reference to restrict verification work) 
 Negative statements (such as statements of system capability not to be provided) 

Important examples of the requirements type attribute include: 
Functional. Functional requirements describe the system or system element functions or tasks to be 
performed. 
 Performance. A requirement that defines the extent or how well, and under what conditions, a function or  task is to be performed. These are quantitative requirements of system performance and are verifiable individually. Note that there may be more than one performance requirement associated with a single function, functional requirement, or task. 
Usability/Quality-in-Use Requirements (for user performance and satisfaction)- Provide the basis for 
the design and evaluation of systems to meet the user needs. Usability/Quality-in-Use requirements 
are developed in conjunction with, and form part of, the overall requirements specification of a 
system. 
 Interface. Interface requirements are the definition of how the system is required to interact with external systems (external interface), or how system elements within the system, including human elements, interact with each other (internal interface).
 Design Constraints. A requirement that limits the options open to a designer of a solution by imposing 
immovable boundaries and limits (e.g., the system shall incorporate a legacy or provided system element, or certain data shall be maintained in an on-line repository). 
 Process requirements. These are stakeholder, usually acquirer or user, requirements imposed through 
the contract or statement of work. Process requirements include: compliance with national, state or local laws, including environmental laws; administrative requirements; acquirer/supplier relationship 
requirements; and specific work directives. Process requirements may also be imposed on a program by 
corporate policy or practice. System or system element implementation process requirements, such as 
mandating a particular design method, are usually captured in project agreement documentation such as contracts, statements of work, and quality plans. 
 Non-Functional. These specify requirements under which the system is required to operate or exist or 
system properties. They define how a system is supposed to be.Quality requirements and human factors 
requirements are examples of this type. 
 Quality Requirements – Include a number of the 'ilities' in requirements to include, for example, 
transportability, survivability, flexibility, portability, reusability, reliability, maintainability, and security. 
The list of non-functional, quality requirements (e.g., “ilities”) should be developed prior to initiating 
the requirements document. This should be tailored to the system(s) being developed. As 
appropriate, measures for the quality requirements should be included as well. 
Human Factors Requirements – State required characteristics for the outcomes of interaction with 
human users (and other stakeholders affected by use) in terms of safety, performance, effectiveness, 
efficiency, reliability, maintainability, health, well-being and satisfaction. These include characteristics 
such as measures of usability, including effectiveness, efficiency and satisfaction; human reliability; 
freedom from adverse health effects. 
