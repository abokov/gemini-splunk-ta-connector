!TBD! - this repo is WIP, please take a look on ADK connector - [splunk-gemini-agent](https://github.com/abokov/splunk-gemini-agent)
# Gemini-Splunk Technical Addon Connector (PoC)

## Executive Summary
This Proof of Concept (PoC) integrates Google's Gemini LLM directly into Splunk Enterprise/Cloud. It enables security analysts and IT ops teams to pass complex logs, alerts, or trace data directly to Gemini from the Splunk Search bar using a custom search command (`| gemini`). 

By bridging Splunk's machine data platform with Google's generative AI, this connector accelerates root cause analysis, incident summarization, and remediation planning.

## Architecture
The connector is built as a Splunk Technology Add-on (TA). It utilizes a Custom Search Command (CSC) written in Python. 
1. **Input:** The user pipes search results into the command (e.g., `index=_internal error | head 5 | gemini`).
2. **Processing:** The Python script (`bin/gemini_analyze.py`) intercepts the raw log text and makes an API call to the Google Generative Language API.
3. **Output:** Gemini's analysis, summarization, or suggested remediation is appended as a new field (`gemini_analysis`) in the Splunk search results.

## Setup Instructions
1. Clone this repository into your Splunk apps directory: `$SPLUNK_HOME/etc/apps/`
2. Install the required Python libraries to the local Splunk Python environment:
   `pip install -r requirements.txt -t $SPLUNK_HOME/etc/apps/TA-gemini-connector/bin/lib/`
3. Restart Splunk.
4. Configure your `GEMINI_API_KEY` within the `gemini_analyze.py` script (or via a secure Splunk credential store for production).
