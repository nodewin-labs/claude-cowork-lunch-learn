# FullEnrich MCP Setup Guide

## Step 1: Create a FullEnrich account

Sign up at [FullEnrich](https://fullenrich.partnerlinks.io/pum64ct0fe4h)

You get **1,000 free credits** after signup — enough for hundreds of contact enrichments.

## Step 2: Get your API key

1. Log into FullEnrich dashboard
2. Go to **Settings → API**
3. Copy your API key

## Step 3: Add FullEnrich MCP to Claude Cowork

1. Open Claude Cowork
2. Go to **Settings → MCP Servers**
3. Click **Add Server**
4. Search for "FullEnrich" or add manually:
   - **Name**: FullEnrich
   - **Type**: HTTP
   - **URL**: provided by FullEnrich MCP documentation
5. Enter your API key when prompted
6. Click **Connect**

## Step 4: Verify it works

In a new conversation, ask Claude:
> "Can you enrich the contact john@example.com?"

If FullEnrich is connected, Claude will return enriched contact data.

## What FullEnrich does in this workshop

FullEnrich finds contact information (email, phone, company data) from minimal inputs. When you run a pre-call brief, Claude uses FullEnrich to fill in missing contact details for your meeting attendees.

## Troubleshooting

- **"MCP not found"**: Verify the MCP server URL and that it is running
- **"Authentication failed"**: Check your API key
- **"No results"**: The contact may not be in FullEnrich's database — try with a LinkedIn URL instead of just an email
