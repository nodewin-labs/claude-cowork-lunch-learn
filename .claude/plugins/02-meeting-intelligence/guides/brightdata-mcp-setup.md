# BrightData MCP Setup Guide

## Step 1: Create a BrightData account

Sign up at [https://get.brightdata.com/a9drujwubyjc](https://get.brightdata.com/a9drujwubyjc)

You get **5,000 free credits** after signup — enough for hundreds of profile lookups.

## Step 2: Get your API key

1. Log into BrightData dashboard
2. Go to **Settings → API Keys**
3. Click **Create API Key**
4. Copy the key — you will need it in the next step

## Step 3: Add BrightData MCP to Claude Cowork

1. Open Claude Cowork
2. Go to **Settings → MCP Servers**
3. Click **Add Server**
4. Search for "BrightData" or add manually:
   - **Name**: BrightData
   - **Type**: HTTP
   - **URL**: provided by BrightData MCP documentation
5. Enter your API key when prompted
6. Click **Connect**

## Step 4: Verify it works

In a new conversation, ask Claude:
> "Can you scrape the LinkedIn profile at linkedin.com/in/example?"

If BrightData is connected correctly, Claude will fetch the profile data.

## What BrightData does in this workshop

BrightData scrapes public web data — in our case, LinkedIn profiles. When you run a pre-call brief, Claude uses BrightData to look up your meeting attendees and pull their current role, company, and recent activity.

## Troubleshooting

- **"MCP not found"**: Make sure the BrightData MCP server is running and the URL is correct
- **"Authentication failed"**: Double-check your API key
- **"No data returned"**: The LinkedIn profile may be private or the URL may be incorrect
