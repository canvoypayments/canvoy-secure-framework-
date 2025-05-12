# Threat Modeling - Do Later Features

| Feature                    | STRIDE              | Threat Description                                 | Likelihood | Impact | Risk Level | Mitigation Strategy                                 |
|---------------------------|---------------------|----------------------------------------------------|------------|--------|------------|-----------------------------------------------------|
| Advanced analytics        | Information Disclosure | Unauthorized access to user behavioral data/data usage | Medium     | Medium | Medium     | Data anonymization and strict access control        |
| AI Recommendation Engine | Tampering            | Manipulation for malicious outcomes                | Medium     | High   | High       | Input validations and integrity checks              |
| Interface in Nigerian languages | Non-repudiation    | Users deny due to mistranslation or misunderstanding | Medium     | Low    | Low        | Legal word legalization, UX testing in native language |