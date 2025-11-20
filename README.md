# SecAlertBench

This repository contains materials from the paper *SecAlertBench: Evaluating Large Language Models for Alert Triage in Network Security Devices.*

## About the Project

The `SecAlertBench` project introduces a systematic evaluation framework, including a real-world labeled dataset, to assess the capabilities of Large Language Models (LLMs) in the critical task of network security alert triage. The goal is to provide a standardized benchmark to measure LLM performance and identify key bottlenecks, thereby helping to address the pervasive issue of alert fatigue in Security Operations Centers (SOCs).

Our full dataset, sourced from the SOCs of large enterprises, contains **17,967** meticulously labeled alert logs.


## Dataset Categories

The alert logs are categorized into four distinct types, reflecting real-world SOC scenarios. This repository contains examples for each category.

*   **Attack Events (AE):** Confirmed malicious activities where an attack was successfully detected. These are high-priority events.
*   **False Positives (FP):** Alerts triggered by entirely benign business activities that were incorrectly flagged as malicious by security systems. This is a major source of noise in SOCs.
*   **Benign Triggers (BT):** Alerts triggered by authorized, non-malicious activities that mimic attack patterns, such as scheduled vulnerability scans or red team exercises.
*   **Informational Events (IE):** Alerts that do not indicate a direct attack but highlight policy violations or risky behaviors, such as the use of weak passwords or outdated protocols.

## Data Format

Each alert is presented as a single JSON object with a standardized schema. This format is designed to be easily parsable and suitable for input into LLMs.

Here is an example of a single alert log (anonymized):

```json
{
  "timestamp": 1747037759,
  "sip": "internal_ip_abc",
  "dip": "10.115.50.29",
  "proto": "http",
  "sport": 46144,
  "dport": 8081,
  "rule_name": "Directory traversal attack",
  "package_data": {
    "request_header": "GET /manage/log/view?filename=/etc/passwd&base=../../../../../../../../ HTTP/1.1\nHost: host_xyz\nUser-Agent: Mozilla/5.0...\n",
    "request_body": "N/A",
    "response_header": "HTTP/1.1 400 Bad Request\nContent-Type: text/plain; charset=utf-8\n",
    "response_body": "400 Bad Request",
    "payload": "filename=/etc/passwd&base=../../../../../../../../"
  }
}
```

### Key Fields:
*   `rule_name`: The name of the security rule that triggered the alert.
*   `package_data`: An object containing the core details of the network packet.
    *   `request_header`/`response_header`: HTTP headers.
    *   `request_body`/`response_body`: The body of the HTTP request/response.
    *   `payload`: The specific part of the data that is most relevant for analysis, often containing the potential attack signature.

## File Structure


```
.
├── data_examples/
│   ├── attack_events.json
│   ├── false_positives.json
│   ├── benign_triggers.json
│   └── informational_events.json
└── README.md
```

## Full Dataset Availability

The complete **SecAlertBench** dataset, comprising all 17,967 labeled alerts, is currently undergoing a final, rigorous anonymization review to ensure full compliance with privacy and confidentiality standards.

**We are committed to releasing the full dataset to the public upon the acceptance of our paper.**

