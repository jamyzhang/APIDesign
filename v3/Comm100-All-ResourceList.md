
# Resource List  - RealtimeConversation 
|Name|EndPoint|Note| 
|---|---|---|
|[Chats](#chats)|/api/v3/realtime/Historys/chats|  | 
|[Offline Messages](#offline-messages)|/api/v3/realtime/Historys/offlineMessages | |
|[Missed & Refused Chats](#get-missed-and-refused-chats-list)|/api/v3/realtime/Historys/missedAndRefusedChats | | 
|[Agent chats](#agent-chats)|/api/v3/realtime/Historys/agentChats | |
|[Campaigns](#campaigns)|/api/v3/realtime/campaigns | | 
|[Installation Code](#installation-code)|/api/v3/realtime/campaigns/{id}/code | | 
|[Chat Button](#chat-button)|/api/v3/realtime/campaigns/{id}/chatButton| | 
|[Chat Window](#chat-window)|/api/v3/realtime/campaigns/{id}/chatWindow| | 
|[Pre-Chat](#pre-chat)|/api/v3/realtime/campaigns/{id}/preChat||
|[Post-Chat](#post-chat)|/api/v3/realtime/campaigns/{id}/postChat| |
|[Offline Message ](#offline-messages)|/api/v3/realtime/campaigns/{id}/offlineMessage|| 
|[Invitation](#invitations)|/api/v3/realtime/campaigns/{id}/invitation|| 
|[Agent Wrapup](#agent-wrapups)|/api/v3/realtime/campaigns/{id}/agentWrapup| |
|[Routing Rules](#routing-rules)|/api/v3/realtime/campaigns/{id}/RoutingRules| | 
|[Language](#languages)|/api/v3/realtime/campaigns/{id}/language| | 
|[Bot](#languages)|/api/v3/realtime/campaigns/{id}/bot| | 
|[Kb Integration](#languages)|/api/v3/realtime/campaigns/{id}/kbIntegration| | 
|[All Campaigns](#languages)|/api/v3/realtime/campaigns/allCampaigns| |
|[Auto allocation](#auto-allocation)|/api/v3/realtime/autoAllocation| settings| 
|[Auto Translation](#auto-translation)|/api/v3/realtime/autoTranslation| settings| 
|[Audio & Video Chat](#audio-video-chat)|/api/v3/realtime/audiovideochat| settings| 
|[Co-browsing](#co-browsing)|/api/v3/realtime/cobrowsing|settings| 
|[Ban list](#bans)|/api/v3/realtime/Bans| settings| 
|[Custom Away Status](#custom-away-status)|/api/v3/realtime/customAwayStatus| settings| 
|[Conversion Actions](#conversion-actions)|/api/v3/realtime/conversionActions | settings | 
|[Segmentations](#visitor-segmentations)|/api/v3/realtime/visitorSegmentations| settings| 
|[Secure Forms](#secure-forms)|/api/v3/realtime/secureForms| settings| 
|[Custom Variables](#custom-variables)|/api/v3/realtime/customVariables|settings |
|[Chat volume ](#agent-chats)|/api/v3/realtime/reports/chatVolume |reports |
|[Chat Source ](#agent-chats)|/api/v3/realtime/reports/chatSource |reports |
|[Queue ](#agent-chats)|/api/v3/realtime/reports/queue |reports |
|[Wait Time ](#agent-chats)|/api/v3/realtime/reports/waitTime |reports |
|[Chat Transfer ](#agent-chats)|/api/v3/realtime/reports/chatTransfer |reports |
|[Availability ](#agent-chats)|/api/v3/realtime/reports/availability |reports |
|[Agent Status ](#agent-chats)|/api/v3/realtime/reports/agentStatus |reports |
|[Agent Performance ](#agent-chats)|/api/v3/realtime/reports/agentPerformance |reports |
|[Workload ](#agent-chats)|/api/v3/realtime/reports/workload |reports |
|[Efficiency ](#agent-chats)|/api/v3/realtime/reports/efficiency |reports |
|[Rating ](#agent-chats)|/api/v3/realtime/reports/rating |reports |
|[Post Chat Survey ](#agent-chats)|/api/v3/realtime/reports/postChatSurvey |reports |
|[Pre-Chat Survey ](#agent-chats)|/api/v3/realtime/reports/prechatSurvey |reports |
|[Wrap-up ](#agent-chats)|/api/v3/realtime/reports/survey |reports |
|[Conversions ](#agent-chats)|/api/v3/realtime/reports/conversions |reports |
|[Manual Invitation ](#agent-chats)|/api/v3/realtime/reports/manualInvitation |reports |
|[Auto Invitation ](#agent-chats)|/api/v3/realtime/reports/autoInvitation |reports |
|[Offline Message ](#agent-chats)|/api/v3/realtime/reports/offlineMessage |reports |
|[Canned Message ](#agent-chats)|/api/v3/realtime/reports/cannedMessage |reports |
|[Real Time ](#agent-chats)|/api/v3/realtime/reports/realTime |reports |




<!-- |[Live Chat Config](#live-chat-config)|/api/v3/realtime/config| | 
|[Attachments](#attachments)|/api/v3/realtime/attachments | (move to public) | 
|[Departments](#departments)|/api/v3/realtime/departments|(move to public)|
|[Canned Messages](#canned-messages)|/api/v3/realtime/cannedMessages|(move to public)| 
|[Canned Message Categorys](#canned-message-categorys)|/api/v3/realtime/cannedMessageCategories|(move to public)| 
|[Agents](#agents)|/api/v3/realtime/agents| |  
|[Visitor SSO Settings](#visitor-sso-settings)|/api/v3/realtime/visitorSSO | settings| 
-->

# Resource List - AnytimeConversation
|Name|EndPoint|Note| 
|---|---|---| 
|[Conversation](#conversation)|/api/v3/anytime/conversations| | 
|[Message](#conversation)|/api/v3/anytime/conversations/{id}/messages| | 
|[Filter](#filter)|/api/v3/anytime/filters| Agent console filters| 
|[Field & Mappings](#field)|/api/v3/anytime/fields| System fields and custom fields | 
|[RoutingRule](#routingrule)|/api/v3/anytime/routingRules||
|[Auto Allocation](#routingrule)|/api/v3/anytime/autoAllocation||
|[Trigger](#routingrule)|/api/v3/anytime/triggers||
|[Working Time & Holidays](#routingrule)|/api/v3/anytime/workingTimeAndHolidays||
|[SLA Policies](#routingrule)|/api/v3/anytime/sLAPolicies||
|[BlockedSender](#blockedsender)|/api/v3/anytime/blockedSenders|Blocked email or domain| 
|[EmailAccount](#emailaccount)|/api/v3/anytime/emailAccounts| Email accounts|
|[IntegrationAccount](#IntegrationAccount)|/api/v3/anytime/IntegrationAccounts| (New)? |  
|[JunkEmail](#junkemails)|/api/v3/anytime/junkEmails| Emails from blocked senders| 
|[Right Now Reports](#reports)|/api/v3/anytime/reports/rightNow| | 
|[Volume Reports](#reports)|/api/v3/anytime/reports/volume|  | 
|[Channel Reports](#reports)|/api/v3/anytime/reports/channel|  | 
|[Efficiency Reports](#reports)|/api/v3/anytime/reports/efficiency|  |
|[Portalconversation](#portalconversation)|/api/v3/anytime/portalconversations|  |
<!-- 
|[Webhooks](#webhooks)|/api/v3/realtime/webhooks | | 
|[Notification](#notification)|/api/v3/anytime/notification| (new)? angent notification to server | 
|[Department](#department)|/api/v3/anytime/departments|(move to public)  |
|[Config](#config)|/api/v3/anytime/configs| Get site settings| 
|[CannedResponse](#cannedresponse)|/api/v3/anytime/cannedResponses|(move to public) |
|[Attachment](#attachment)|/api/v3/anytime/attachments|(move to public)?| -->

# Resource List - Bot
|Name|EndPoint|Note| 
|---|---|---| 
| [Bot](#bot) | /api/v3/aI/bots |
| [Intent](#intent) | /api/v3/aI/bots/{bot_id}/intents |  
| [Entity](#entity) | /api/v3/aI/bots/{bot_id}/entities |  
| [Category](#category) | /api/v3/aI/bots/{bot_id}/categories |  
| [Smart Trigger](#smart-trigger) | /api/v3/aI/bots/{bot_id}/smartTriggers |  
| [Quick Reply](#quick-reply) | /api/v3/aI/bots/{bot_id}/quickReplies |  
| [Learning Question](#learning-question) | /api/v3/aI/bots/{bot_id}/learningquestions | 
| [Report](#report) | /api/v3/aI/bots/{bot_id}/reports | 
| [General](#general) | /api/v3/aI/genaral |
| [Agent Bot Setting](#agent-bot-setting) | /api/v3/aI/agentBot/setting |
| [Agent Bot Word Weight](#agent-bot-word-weight) | /api/v3/aI/agentBot/wordWeight |
| [Agent Bot Synonym](#agent-bot-synonym) | /api/v3/aI/agentBot/synonyms | 
| [Agent Bot Learning Question](#agent-bot-learing-question) | /api/v3/aI/agentBot/learningQuestions |  
| [Agent Bot Suggestion](#agent-bot-suggestion) | /api/v3/aI/agentBot/questionSuggestions/query | 

# Resource List - Common
|Name|EndPoint|Note| 
|---|---|---| 
|[Contact](#contact)| /api/v3/contacts|| 
|[Contact identities](#contact)| /api/v3/contacts/{Id}/identities|| 
|[Visitor SSO Settings](#visitor-sso-settings)|/api/v3/visitorSSO | 从realtime转移到公共模块| 
|[Agent](#agent)| /api/v3/agents||
|[Site](#site)| /api/v3/sites|Account & Billing|
|[Tag](#tag)|/api/v3/tags|从anytime转移过来，realtime暂不实现| 
|[Canned Messages](#agent)|/api/v3/cannedMessages|从anytime和realtime合并并转移到公共模块|
|[Canned Message Categorys](#canned-message-categorys)|/api/v3/cannedMessageCategories|从anytime和realtime移交,需要合并数据|
|[Departments](#departments)|/api/v3/departments|从anytime和realtime合并并转移到公共模块|
|[Attachments](#attachments)|/api/v3/attachments|从anytime和realtime合并并转移到公共模块|
|[Credit Card Masking](#credit-card-masking)|/api/v3/creditcardMasking||
|[Password Policy](#password-policy)|/api/v3/passwordPolicys||
|[Audit Log](#audit-log)|/api/v3/auditLogs||
|[Agent Single Sign-On](#agent-single-sign-on)|/api/v3/agentSingleSignOn||
|[Agent reports ](#agent-reports)|/api/v3/reports/agentReports |Availability/Canned Message  |
|[webhooks](#webhooks)|/api/v3/webhooks |  |



