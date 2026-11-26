# مهارات Anthropic المثبتة (26 نوفمبر 2026)

## من anthropics/skills
xlsx وpptx وdocx وpdf وinternal-comms: إنشاء ملفات Excel وPowerPoint وWord وPDF، والمراسلات الداخلية.

## من anthropics/knowledge-work-plugins (رخصة Apache 2.0، انظر ANTHROPIC-KWP-LICENSE.txt)
- **أسماء المجلدات:** `<الإضافة>-<المهارة>`.
- **المهارات المثبتة (27):**
  - المبيعات: sales-call-prep، وsales-handle-objection، وsales-pipeline-review، وsales-win-loss-review، وsales-account-research، وsales-customer-health.
  - القانون: legal-compliance-check، وlegal-review-contract، وlegal-legal-risk-assessment، وlegal-vendor-check.
  - الموارد البشرية: human-resources-onboarding، وhuman-resources-performance-review، وhuman-resources-interview-prep، وhuman-resources-recruiting-pipeline.
  - خدمة العملاء: customer-support-ticket-triage، وcustomer-support-draft-response، وcustomer-support-kb-article، وcustomer-support-customer-escalation.
  - البيانات: data-analyze، وdata-build-dashboard، وdata-validate-data.
  - العمليات: operations-risk-assessment، وoperations-process-doc، وoperations-status-report.
  - المنتج: product-management-write-spec، وproduct-management-roadmap-update، وproduct-management-metrics-review.
- **تنبيه:** بعض هذه المهارات مكتوبة على الأنظمة الأمريكية، كالقانون والموارد البشرية. **أنظمة المملكة تغلب دائماً:** نظام العمل، ونظام حماية البيانات الشخصية، ولائحة هيئة الاتصالات، ونظام الشركات.

## ما لم يُثبّت ولماذا
- **prompt-eng-interactive-tutorial:** دورة تعليمية لا مهارة. طُبّقت مبادئها كقوانين لكتابة الموظفين في مركز القيادة.
- **claude-quickstarts:** قوالب برمجية لا مهارات. أُخذ منها customer-support-agent وfinancial-data-analyst كمرجع لفريق الهندسة («سمّ»).
- **claude-plugins-official:** سجل إضافات Claude Code، تُثبّت بالأمر `/plugin install <اسم>@claude-plugins-official`. المفيد لنا منها:
  - `security-guidance` و`code-review`: لمراجعة كود Sahal.
  - `telegram` (في external_plugins): للتواصل مع Claude من تيليجرام.
- **launch-your-agent:** يحتاج حساب Claude API مدفوعاً (Managed Agents). يُعاد النظر فيه عند فتح حساب API.
- **claude-code-playground:** تجارب غير رسمية بلا مهارات قابلة للتثبيت.
