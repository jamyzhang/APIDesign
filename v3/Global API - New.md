# Global RestFUL API
<div>

  | Change Version | API Version | Change nots | Change Date | Author |
  | - | - | - | - | - |
  | 1.0 | v3 |  | 2020-02-17 | Hardy |

# Summary
  - Global
    - [site](#site) Get PUT
    - [agent](#agent) include role, permission, shift  Get ../agents
        - [permission](#permission)
        - [shift](#shift)
    - [role](#role) include agent, permission
        - [agent](#agent)
        - [permission](#permission)
    - [department](#department) include agent, shift
        - [agent](#agent)  ../departments/{depid}/agents
        - [shift](#shift)
    - [contact](#contact)
        - [contact identity](#contact-identity)
    - [visitor](#visitor)  GetList, GetbyId
    - [public canned message category](#public-canned-message-category)
    - [public canned message](#public-canned-message)
    - [private canned message category](#private-canned-message-category)
    - [private canned message](#private-canned-message)
    - [agent away status](#agent-away-status)
    - [whitelisted login IP range](#whitelisted-login-ip-range)
    - [agent sso](#agent-sso) include agent Get, PUT
    - [visitor sso](#visitor-sso) Get, PUT
    - [shift](#shift) 
    - [oauth client](#oauth-client) Get  ? 这个接口怎么处理
    - [audit log](#audit-log) include agent;  GetList（分页） Get
  

# Site
  You need `Manage Site` permission to manage site 
  + `GET /api/v3/globalSettings/site` - [Get profile of a single site](#get-site-info)
  + `PUT /api/v3/globalSettings/site` - [Update profile of a site](#update-site-info)

# Agent
  + `GET /api/v3/globalSettings/agents` - [Get a list of agents in site](#get-all-agents)  include department, role
  + `GET /api/v3/globalSettings/agents/{id}` - [Get an agent by id](#get-an-agent)  include department, role
  + `GET /api/v3/globalSettings/roles/{roleId}/agents` - [Get a list of agents by role id](#get-an-agent)  include department, role
  + `GET /api/v3/globalSettings/departments/{departmentId}/agents` - [Get a list of agents by department id](#get-an-agent)  include department, role
  + `GET /api/v3/globalSettings/agents/me` - [Get current agent](#get-current-agent)  include department, role
  + `POST /api/v3/globalSettings/agents` - [create a new agent](#get-all-agents)
  + `POST /api/v3/globalSettings/agents/{id}:unlock` - [unlock the agent](#get-all-agents)
  + `POST /api/v3/globalSettings/agents/{id}:changePassword` - [Admin set an agent's password](#get-all-agents)
  + `PUT /api/v3/globalSettings/agents/{id}` - [update an agent](#get-all-agents)
  + `PUT /api/v3/globalSettings/agents/me` - [update current agent](#get-all-agents)
  + `POST /api/v3/globalSettings/agents/me:changePassword` - [Change own password](#get-all-agents)
  + `DELETE /api/v3/globalSettings/agents/{id}` - [delete an agent](#get-all-agents)

# Role
  + `GET /api/v3/globalSettings/roles` - [Get a list of roles in site](#get-all-roles)  include agent, permission
  + `GET /api/v3/globalSettings/roles/{id}` - [Get a role by id](#get-an-agent) include agent, permission
  + `POST /api/v3/globalSettings/roles` - [create a new role](#get-all-agents)
  + `PUT /api/v3/globalSettings/roles/{id}` - [update a role](#get-all-agents)
  + `DELETE /api/v3/globalSettings/roles/{id}` - [delete a role](#get-all-agents)

# Department
  + `GET /api/v3/globalSettings/departments` - [Get a list of departments in site](#get-all-departments) include agent
  + `GET /api/v3/globalSettings/departments/{id}` - [Get a department by id](#get-an-agent) include agent
  + `POST /api/v3/globalSettings/departments` - [create a new department](#get-all-agents)
  + `PUT /api/v3/globalSettings/departments/{id}` - [update a department](#get-all-department)
  + `DELETE /api/v3/globalSettings/departments/{id}` - [delete a department](#get-all-departments)

# Permission
  + `GET /api/v3/globalSettings/roles/{roleId}/permission` - [Get role permission](#get-an-agent)
  + `GET /api/v3/globalSettings/agents/{agentId}/permission` - [Get agent permission](#get-an-agent)
  + `GET /api/v3/globalSettings/agents/{agentId}/permission:effective` - [Get a list of agent's effective permissions,including the permissions of the agent and the permissions of the roles which the agent belongs to](#get-an-agent) 
  + `PUT /api/v3/globalSettings/roles/{roleId}/permission` - [update role permission](#get-all-agents)
  + `PUT /api/v3/globalSettings/agents/{agentId}/permission` - [update agent permission](#get-all-agents)
  

# Shift
  //?  include : entity name or field name
  // auto code: entity name
  + `GET /api/v3/globalSettings/shifts` - [Get a list of shifts in site](#get-all-departments) include department, agent
  + `GET /api/v3/globalSettings/departments/{departmentId}/shifts` - [Get a list of shift by department id](#get-an-agent) 
  + `GET /api/v3/globalSettings/agents/{agentId}/shifts` - [Get a list of shifts by agent id](#get-an-agent)
  + `GET /api/v3/globalSettings/shifts/{id}` - [Get a shift by id](#get-a-shift) inclde department, agent 
  + `POST /api/v3/globalSettings/shifts` - [create a new shift](#get-all-agents)
  + `PUT /api/v3/globalSettings/shifts/{id}` - [update a shift](#get-all-department)
  + `DELETE /api/v3/globalSettings/shifts/{id}` - [delete a shift](#get-all-departments)

# Contact
?? 根据ssoId 查询 contact (查看 zendesk api)
  + `GET /api/v3/globalSettings/contacts` - [Get a list of contacts in site](#get-all-contacts)  通过 query string 来实现复杂查询
  + `GET /api/v3/globalSettings/contacts/{id}` - [Get a contact by id](#get-an-contact)
  + `POST /api/v3/globalSettings/contacts` - [create a new contact](#get-all-agents)
  + `PUT /api/v3/globalSettings/contacts/{id}` - [update a contact](#get-all-agents)
  + `DELETE /api/v3/globalSettings/contacts/{id}` - [delete a contact](#get-all-agents)

# Contact Identity
  + `GET /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [Get a list of contactIdentities in a contact](#get-all-agents)
  + `GET /api/v3/globalSettings/contactIdentities/{id}` - [Get a contactIdentity by id](#get-an-agent)
  + `POST /api/v3/globalSettings/contacts/{contactId}/contactIdentities` - [create a new contactIdentity](#get-all-agents)
  + `PUT /api/v3/globalSettings/contactIdentities/{id}` - [update a contactIdentity](#get-all-agents)
  + `DELETE /api/v3/globalSettings/contactIdentities/{id}` - [delete a contactIdentity](#get-all-agents)

# Visitor
  + `GET /api/v3/globalSettings/visitors` - [Get a list of visitors in site](#get-all-visitors)
  + `GET /api/v3/globalSettings/visitors/{id}` - [Get a visitor by id](#get-a-visitors)  

# Public Canned Message Category
  + `GET /api/v3/globalSettings/publicCannedMessageCategories` - [Get a list of publicCannedMessageCategories in site](#get-all-contacts)
  + `GET /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [Get a publicCannedMessageCategory by id](#get-an-contact)
  + `POST /api/v3/globalSettings/publicCannedMessageCategories` - [create a new publicCannedMessageCategory](#get-all-agents)
  + `PUT /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [update a publicCannedMessageCategory](#get-all-agents)
  + `DELETE /api/v3/globalSettings/publicCannedMessageCategories/{id}` - [delete a publicCannedMessageCategory](#get-all-agents)

# Public Canned Message 
  + `GET /api/v3/globalSettings/publicCannedMessages` - [Get a list of publicCannedMessages in site](#get-all-contacts) include publicCannedMessageCategory
  + `GET /api/v3/globalSettings/publicCannedMessages/{id}` - [Get a publicCannedMessage by id](#get-an-contact) include publicCannedMessageCategory
  + `POST /api/v3/globalSettings/publicCannedMessages` - [create a new publicCannedMessage](#get-all-agents)
  + `PUT /api/v3/globalSettings/publicCannedMessages/{id}` - [update a publicCannedMessage](#get-all-agents)
  + `DELETE /api/v3/globalSettings/publicCannedMessages/{id}` - [delete a publicCannedMessage](#get-all-agents)

# Private Canned Message Category
  + `GET /api/v3/globalSettings/privateCannedMessageCategories` - [Get a list of privateCannedMessageCategories in site](#get-all-contacts)
  + `GET /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [Get a privateCannedMessageCategory by id](#get-an-contact)
  + `POST /api/v3/globalSettings/privateCannedMessageCategories` - [create a new privateCannedMessageCategory](#get-all-agents)
  + `PUT /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [update a privateCannedMessageCategory](#get-all-agents)
  + `DELETE /api/v3/globalSettings/privateCannedMessageCategories/{id}` - [delete a privateCannedMessageCategory](#get-all-agents)

# Private Canned Message
  + `GET /api/v3/globalSettings/privateCannedMessages` - [Get a list of privateCannedMessages in site](#get-all-contacts) include privateCannedMessageCategory
  + `GET /api/v3/globalSettings/privateCannedMessages/{id}` - [Get a privateCannedMessage by id](#get-an-contact) include privateCannedMessageCategory
  + `POST /api/v3/globalSettings/privateCannedMessages` - [create a new privateCannedMessage](#get-all-agents)
  + `PUT /api/v3/globalSettings/privateCannedMessages/{id}` - [update a privateCannedMessage](#get-all-agents)
  + `DELETE /api/v3/globalSettings/privateCannedMessages/{id}` - [delete a privateCannedMessage](#get-all-agents)

# Agent Away Status
  + `GET /api/v3/globalSettings/agentAwayStatuses` - [Get a list of agentAwayStatuses in site](#get-all-contacts)
  + `GET /api/v3/globalSettings/agentAwayStatuses/{id}` - [Get an agentAwayStatus by id](#get-an-contact)
  + `POST /api/v3/globalSettings/agentAwayStatuses` - [create a new agentAwayStatus](#get-all-agents)
  + `PUT /api/v3/globalSettings/agentAwayStatuses/{id}` - [update an agentAwayStatus](#get-all-agents)
  + `DELETE /api/v3/globalSettings/agentAwayStatuses/{id}` - [delete an agentAwayStatus](#get-all-agents)

# Whitelisted Login IP Range
  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges` - [Get a list of whitelistedLoginIPRanges in site](#get-all-contacts) 
  + `GET /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [Get a whitelistedLoginIPRange by id](#get-an-contact) 
  + `POST /api/v3/globalSettings/whitelistedLoginIPRanges` - [create a new whitelistedLoginIPRange](#get-all-agents)
  + `PUT /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [update a whitelistedLoginIPRange](#get-all-agents)
  + `DELETE /api/v3/globalSettings/whitelistedLoginIPRanges/{id}` - [delete a whitelistedLoginIPRange](#get-all-agents)

# Agent SSO  
  //ER修改: 证书不用File 用string
  + `GET /api/v3/globalSettings/agentSSO` - [Get Agent SSO](#get-an-agent) 
  + `PUT /api/v3/globalSettings/agentSSO` - [update Agent SSO](#get-all-agents)

# Visitor SSO  
  //ER修改: 证书不用File 用string
  + `GET /api/v3/globalSettings/visitorSSO` - [Get Visitor SSO](#get-visitor-sso)  include campaign
  + `PUT /api/v3/globalSettings/visitorSSO` - [update Visitor SSO](#update-visitor-sso)
 
# Audit Log
  + `GET /api/v3/globalSettings/auditLogs` - [Get audit logs list](#get-an-agent) include agent
  https://www.comm100.com/doc/api/introduction.htm#/Account?id=audit-logs


</div>
&#32;