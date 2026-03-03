# AWS IAM Architecture – Designing Identity Boundaries in Cloud Systems

Identity is the control plane of cloud security.

Before deploying compute, storage, or networking resources, cloud architects must design identity boundaries intentionally. AWS Identity and Access Management (IAM) is the foundation of access governance in AWS.

---

## 1. What is AWS IAM?

AWS Identity and Access Management (IAM) is a **global service** that controls authentication and authorization across AWS resources.

IAM manages:

- Users
- Groups
- Policies
- Roles
- Access credentials

The root account is created by default when an AWS account is created.  
It should never be used for day-to-day operations.

**Architectural Principle**

Root account usage should be restricted to:

- Initial account setup
- Billing configuration
- Emergency recovery scenarios

Never use it for operational work.

---

## 2. IAM Core Components

### 2.1 Users

IAM Users represent individual people or systems requiring AWS access.

Best practices:

- One physical user = One IAM user
- Avoid shared credentials
- Enforce strong password policy
- Enforce MFA

Users can:

- Belong to multiple groups
- Have policies attached directly (not recommended at scale)

At scale, identity should be structured — not improvised.

---

### 2.2 Groups

Groups are collections of IAM users.

Important characteristics:

- Groups contain users only
- Groups cannot contain other groups
- Permissions should be assigned to groups (not individuals)

Architectural benefit:

Group-based permission assignment improves governance, reduces duplication, and simplifies scaling across teams.

---

### 2.3 Policies

Policies define permissions in IAM.

Policies determine:

- What actions are allowed or denied
- On which resources
- Under what conditions

IAM follows the **Principle of Least Privilege**:

Only grant the permissions necessary to perform required tasks.

Poorly scoped permissions expand security blast radius.

---

## 3. IAM Policy Structure

An IAM policy consists of:

- **Version** – Policy language version
- **Statement** – One or more permission statements

Each Statement includes:

- **Sid** (optional) – Statement identifier
- **Effect** – `Allow` or `Deny`
- **Principal** – Entity the policy applies to
- **Action** – List of API actions
- **Resource** – Target resource(s)
- **Condition** (optional) – Conditional logic

### Example Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "elasticloadbalancing:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:ListMetrics",
        "cloudwatch:GetMetricStatistics",
        "cloudwatch:Describe*"
      ],
      "Resource": "*"
    }
  ]
}
```

IAM policies define:

- Effect (Allow or Deny)
- Action (API operations permitted)
- Resource (Target resource)
- Condition (Optional constraints)
- Principal (Who the policy applies to)

From an architectural standpoint:

Policies define your access boundaries.

The tighter and more intentional the policy design, the smaller the potential blast radius.

---

## 4. Principle of Least Privilege

Least privilege means:

- Grant minimal permissions required
- Avoid wildcard access
- Continuously audit permissions

Over-permissioned identities increase:

- Lateral movement risk
- Accidental deletion risk
- Compliance violations
- Insider threat exposure

Least privilege is not just a best practice — it is structural security discipline.

---

## 5. Password Policies & MFA

Strong authentication reduces attack surface.

Recommended password controls:

- Minimum length
- Uppercase and lowercase characters
- Numbers
- Special characters
- Password expiration
- Prevent password reuse

### Multi-Factor Authentication (MFA)

Authentication = Password + Physical/Virtual device.

MFA should be mandatory for:

- Root account
- Administrative users
- Production access accounts

Identity security begins at authentication.

---

## 6. Access Methods: Console, CLI, SDK

Users access AWS through:

- AWS Management Console
- AWS CLI
- AWS SDK

Programmatic access uses:

- Access Key ID
- Secret Access Key

Architectural rule:

Avoid long-lived static credentials whenever possible.

Prefer:

- IAM Roles
- Temporary credentials
- Role assumption
- Federated identity providers

---

## 7. IAM Roles – Preferred Access Model

IAM Roles allow AWS services or users to assume temporary permissions.

Common examples:

- EC2 Instance Roles
- Lambda Execution Roles
- CloudFormation Roles

Benefits:

- No embedded secrets
- Automatic credential rotation
- Reduced secret sprawl
- Safer automation pipelines

At scale, roles should replace static credentials entirely.

---

## 8. IAM Audit & Governance Tools

IAM provides built-in auditing capabilities.

### IAM Credentials Report

Provides account-level visibility into:

- Password usage
- MFA status
- Access key age
- Credential rotation status

### IAM Access Advisor

Provides user-level insights:

- Services granted
- Last accessed timestamps

Governance requires continuous visibility and periodic review.

---

## 9. IAM Best Practices

- Do not use root account operationally
- One user per individual
- Assign permissions to groups
- Enforce strong password policy
- Enforce MFA
- Use IAM roles for services
- Avoid sharing access keys
- Regularly audit permissions
- Remove unused credentials

Security is a continuous process, not a configuration step.

---

## 10. Architectural Perspective

IAM is not about granting access.

It defines:

- Security boundaries
- Operational blast radius
- Governance structure
- Compliance posture
- Automation safety

Well-designed IAM:

- Limits lateral movement
- Reduces insider risk
- Protects production environments
- Enables safe CI/CD pipelines

Poor IAM design introduces systemic risk.

---

## 11. Conclusion

Scalable cloud systems require:

- Infrastructure resilience
- Network segmentation
- Data protection
- Identity discipline

IAM is the foundation of cloud identity architecture.

Security architecture begins with identity architecture.
