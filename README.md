# LensAI

AI-powered quality inspection built for Indian MSMEs

Submitted for the Elixir Case Competition 2026 (Startup India x MarkSoc, Shaheed Bhagat Singh College)

Case prompt: What is the most important AI intervention in manufacturing that will create massive ripple effects on the Indian economy?

## The problem we're going after

India's manufacturing sector isn't small by any measure — it added roughly ₹41.69 lakh crore to GVA in FY 2024-25, about 17% of GDP, and the government wants that number at 25% by 2030. MSMEs are doing most of the heavy lifting here: they're responsible for around 35% of manufacturing output and nearly half of India's exports, while employing over 110 million people.

The catch is that scale hasn't come with standard. Manual quality inspection in most MSME facilities still catches only 80-85% of defects, and that gap shows up directly in the numbers — export batches getting rejected at 10-15% of shipment value, single FDA flags costing pharma exporters ₹5-50 crore in lost revenue, ceramic units in Morbi losing entire buyer contracts over colour variation. Across textiles, auto components, pharma, steel and ceramics, we estimated the defect-driven export losses at around ₹4,300 crore a year (full sector-by-sector math is in the appendix of the deck).

The interesting part is that the government has already started pushing MSMEs toward better quality benchmarks through schemes like Zero Defect Zero Effect. ZED certifications went from 3,160 in 2022-23 to over 1.76 lakh in 2023-24 — a 55x jump in two years. Demand for better quality control is already there. What's missing is a way for a small manufacturer to actually afford it.

## Why existing solutions don't work for this segment

Machine vision systems from global players like Cognex or Keyence assume you have industrial-grade cameras, controlled lighting rigs, and thousands of labelled defect images to train a model on. That's a reasonable ask for a large auto OEM. It's not reasonable for a textile unit in Tirupur running on thin margins, or a steel re-roller in a Tier-2 cluster with inconsistent power and lighting.

Even the closer Indian competitors fall short in different ways. Robro Systems is hardware-first and largely textile-focused — every new customer means a physical retrofit and custom calibration, which doesn't scale well past a certain point. Qualitas Technologies has a technically strong platform, but by their own account, getting a production-grade deployment tuned can take months, and the interface is English-only, which cuts out a large share of actual shop-floor operators.

## What LensAI does differently

The core idea is to strip out everything that makes machine vision expensive and slow to deploy, without giving up accuracy.

A LensAI setup uses an ordinary smartphone-grade camera, in the ₹8,000-15,000 range, mounted above the line with no rewiring and no special lighting requirement. Instead of needing thousands of labelled images, the model learns what a "good" product looks like from just 20-30 sample photos taken by the owner on day one. It's typically live and flagging defects by day two.

On the technical side, we're using a three-layer approach: an EfficientNet-B0 / ResNet-50 backbone for feature extraction, a YOLOv8-nano detection layer that's light enough to run at 15-30 FPS on standard MSME conveyor speeds, and a few-shot Siamese/prototypical learning layer that handles the "learn from almost nothing" part by flagging deviations in embedding space rather than requiring exhaustive labelled training data. The whole thing runs on edge hardware like a Raspberry Pi or Jetson Nano, so it doesn't fall over when the internet connection does — which matters a lot in Tier-2 and Tier-3 clusters.

Alerts go out over WhatsApp, in the operator's language, rather than through a dashboard nobody on the shop floor is going to check. And every deployment feeds into a shared, federated model — so as more units across a cluster come online, the system gets better at spotting defects specific to that industry, without any single customer having to hand over proprietary data. That federated learning loop is really the long-term moat, since it's not something a competitor can replicate just by copying the product.

## Business model and numbers

Pricing is hybrid: a base SaaS fee of around ₹40,000/month, plus usage-based charges tied to inspection volume, with an optional outcome-based component for customers who'd rather pay based on measured defect reduction. Put together, we modelled that out to roughly ₹16 lakh in annual revenue against about ₹5 lakh in annual cost per customer, which gets to a contribution margin near 69%.

The unit economics work out to a payback period of about 4 months, an LTV/CAC ratio of 5.5, and an ROI in the 6-8x range depending on how much of the defect reduction actually gets captured. These numbers are built off industry benchmarks (cited in the appendix) rather than assumptions we made up, though obviously real-world figures would need validation through pilots.

## How we'd roll this out

We're not trying to hit all six verticals on day one. The plan is staged:

Phase 1 (0-8 months) starts with automotive component manufacturers, mainly because defects there tend to be binary (a crack is a crack) which makes accuracy validation much cleaner, and there are accessible clusters like Rajkot and Pune MIDC to pilot in.

Phase 2 (8-24 months) extends into textiles, pharma and ceramics once the core system has proven itself, building out a distributor network rather than relying purely on direct sales.

Phase 3 (24-40 months) is about broader domestic coverage — bringing in electronics/PCB and steel, and integrating with government portals so ZED compliance data can flow through automatically.

## Risks we're aware of

A few things could genuinely derail this. Shop floor owners might just not trust an AI system over their own eyes, which is why the pilot approach leans on a 90-day free trial and fast, visible ROI rather than asking for buy-in upfront. Lighting conditions on real factory floors are inconsistent, so the model has to be trained on augmented data that simulates that variability, with human review kept in the loop for low-confidence flags rather than auto-rejecting anything. Connectivity in Tier-2/3 clusters can be patchy, which is part of why inference has to run fully on-edge rather than depending on the cloud. And there's a real possibility that Robro or Qualitas simply copy the few-shot approach — our answer to that is that the federated data moat takes time to build regardless, and the vernacular/WhatsApp layer isn't something you can bolt on as a feature, it requires rethinking the product from the ground up.

## Where this leads

If this works the way we think it does, the impact isn't just about fewer rejected shipments. It changes what quality-control jobs look like on the shop floor (line supervisors and calibration technicians instead of pure manual inspectors), it helps Tier-2 suppliers actually qualify for OEM contracts that require certifications like IATF 16949, and more broadly it's a small but real piece of India's case for being a credible "China+1" manufacturing destination — because reliable, auditable quality is exactly what that story depends on.

---

All figures, sources, and detailed unit economics referenced above are documented in the appendix of the full presentation deck.
