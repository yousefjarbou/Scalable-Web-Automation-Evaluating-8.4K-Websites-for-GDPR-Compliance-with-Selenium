# **Scalable Web Automation: Evaluating 8.4K Websites for GDPR Compliance with Selenium**
### **Evaluating GDPR Compliance of Educational Sector Websites January-2025**  
### **A Research Project in Collaboration with Princess Sumaya University for Technology (PSUT)**  

## **Project Overview**  
This project investigates GDPR compliance across **educational websites**, focusing on their cookie consent mechanisms. We aim to **analyze, detect, and evaluate** whether these websites adhere to the **General Data Protection Regulation (GDPR)** by properly handling **cookie consent** and ensuring user privacy.

Our dataset originates from [**The Majestic Million**](https://majestic.com/reports/majestic-million?domain=&majesticMillionType=2&tld=paris&oq=&canUseDefault=), a publicly available list of the most visited websites globally. We specifically targeted **8,483 educational sector websites**, applying two approaches to test their compliance.

The project was developed in partnership with:
- **Sana Mourad & Aya Aljabali**, Master's students at PSUT, who conducted a study on **GDPR compliance in the education sector** and selected **The Majestic Million** dataset for evaluation.
- **Yousef Jarbou**, a **Computer Engineer** who implemented the research into functional **automated testing frameworks**, creating two approaches:  
  - **Approach 1: Automating GDPR compliance checks using [2GDPR](https://2gdpr.com/).**
  - **Approach 2: Developing a custom Selenium-based tool for cookie consent evaluation.**

---

## **Approach 1: 2GDPR Scraper**

Our **first approach** leveraged the [**2GDPR website**](https://2gdpr.com/), a tool that automates GDPR compliance checks based on predefined criteria. The methodology involved:

1. **Extracting websites from the dataset**:
   - We started with a dataset of 8,483 educational URLs derived from "The Majestic Million."
   - The URLs were extracted and fed into the automation script.

2. **Automating interactions with 2GDPR using Selenium**:
   - Navigating to the **2GDPR** site.
   - Entering each URL into the website’s input field.
   - Simulating button clicks to initiate the compliance check.

3. **Extracting results from HTML content**:
   - Results were extracted by parsing the HTML of the results page.
   - We analyzed **icons and colors** on the screen:
     - **Green icons** indicated GDPR compliance.
     - **Red icons** flagged non-compliance.
   - A binary output (e.g., `[1, 0, 1, 1, 1]`) was generated for each website, representing the outcomes of the compliance checks.

4. **Challenges Encountered**:
   - **Rate Limits & Blocking**:
     - The 2GDPR website imposed rate limits, which triggered CAPTCHA challenges and sometimes blocked requests entirely.
   - **Dynamic Content Loading**:
     - Results were not static and required repeated checks to confirm when the data was fully loaded.
   - **Scalability Issues**:
     - Processing a large number of URLs proved to be unsustainable due to dependencies on the third-party website.

5. **How We Tried to Overcome These Challenges**:
   - **Mimicking Human Behavior**:
     - Introduced **randomized delays** between requests (e.g., 0.5 to 2 seconds).
     - Added **periodic longer pauses** after every 20 URLs to reduce detection.
   - **Improved XPath Selection**:
     - Used alternative XPath methods to locate elements more reliably.
   - **Retry Mechanisms**:
     - Implemented logic to retry failed requests due to timeouts or rate limits.
   - **Dynamic Page Detection**:
     - Added waiting mechanisms to detect when the dynamic content was fully loaded before extracting results.
   - **Splitting Data into Batches**:
     - To overcome rate limits and blocking, we **split the dataset into smaller batches** and distributed them across **multiple devices and networks**:
       - Batches were run on different IP ranges (e.g., **home Wi-Fi, university Wi-Fi, mobile hotspot**), minimizing detection by the website.

6. **Partial Success (1,200 Websites Completed)**:
   - Despite the challenges, we successfully processed **1,200 URLs out of the 8,483** in the dataset.
   - The results included:
     - **Acceptance Status**: Whether the website passed or failed compliance checks.
     - **Green Icon Count**: The number of compliance indicators passed.
     - **Binary Check Results**: A 5-element binary representation of the checks performed.

7. **Limitations of Approach 1**:
   - The reliance on **2GDPR** as a third-party tool limited scalability and introduced potential reliability risks.
   - The dynamic loading and frequent rate-limiting added significant delays to processing.

### **Why We Transitioned to Approach 2**
While Approach 1 demonstrated that automation could extract GDPR compliance data, it became evident that relying on a third-party tool like **2GDPR** wasn’t sustainable for a larger-scale dataset. This realization led us to develop our custom **GDPR compliance checker tool** in **Approach 2**, which offered greater control, flexibility, and scalability.

---

## **Approach 2: Custom Selenium-Based GDPR Compliance Tool**
To **overcome the limitations** of **Approach 1**, we built a **fully automated GDPR compliance checker** from scratch.  

### **How Our Custom Tool Works**
1. **Directly visits each website** from our dataset.
2. **Detects cookie consent banners** automatically using **advanced XPath selectors**.
3. **Identifies & interacts with consent buttons**:
   - **“Accept All”**, **“Reject All”**, and **Granular Consent Options**.
4. **Captures Cookies Before & After Consent**:
   - Collects cookies **before clicking the consent button**.
   - Collects cookies **after clicking the consent button**.
   - **Compares the difference** to check if cookies are set **before consent is given**.
5. **Logs and stores results in a structured format**:
   - **Website URL**
   - **Compliance Status** (Compliant, Non-Compliant, Partially Compliant)
   - **Granular Consent Availability**
   - **Number of Cookies Before & After Consent**

### **How We Improved on Approach 1**
 **Directly analyzed websites** instead of relying on an external tool.  
 **Handled hidden cookie banners** by searching for **keywords and alternative selectors**.  
 **Used CDP (Chrome DevTools Protocol)** to capture network cookies.  
 **Made detection more accurate** by identifying **specific consent buttons**.  

### **Optimizing Processing Time**
To handle the large dataset efficiently:
- **Batch Processing**:
  - The dataset was split into **43 batches**, each containing **200 URLs**.
  - Each batch took approximately **1.5 hours** to process.
- **Parallel Execution**:
  - Ran batches across **three different devices**, each handling **14 browser tabs in parallel**.
  - This strategy allowed us to process the entire dataset of **8,453 websites in under 2 hours**.

### **Final Results**
 **Successfully analyzed 8,453 websites.**  
 **Overcame the issues from 2GDPR and built a fully automated GDPR checker.**  
 **Identified major trends in non-compliance, such as setting cookies before consent.**  

---

## **Acknowledgments**
This project was developed in collaboration with:
- **Sana Mourad & Aya Aljabali** – Research & dataset selection.
- **Yousef Jarbou** – Implementation & tool development.
- **Dr. Mu'awya Al-Dala'ien** – Supervision & guidance.

---

## **Conclusion**
This research **bridged the gap** between **GDPR policy enforcement** and **technical evaluation**, providing **actionable insights** into cookie compliance. The two approaches illustrate **how automation can be leveraged** to conduct large-scale privacy audits.

Through **perseverance and technical problem-solving**, we **overcame obstacles**, **built a scalable solution**, and **contributed to GDPR research** in the educational sector.
