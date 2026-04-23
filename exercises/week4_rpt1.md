# Week 4: Learn and experience SAP-RPT-1 model

Welcome to week 4 of April's Developer Challenge on AI! Over the past three weeks you've built up a solid toolkit; grounding with RAG, autonomous agents, and tool-equipped reasoning. This week takes a different turn: instead of working with large language models, you'll explore **SAP-RPT-1**, a foundation model purpose-built for structured, tabular enterprise data.

While LLMs excel at understanding and generating text, many real-world business problems revolve around tables and rows like sales forecasts, churn predictions, anomaly detection. RPT-1 is designed exactly for those use cases, letting you get predictive insights from your enterprise data without the overhead of traditional ML pipelines.

## What You'll Achieve

By working through this exercise, you'll learn how to:

- **Understand RPT-1's approach**: See how a transformer model can be applied to structured/tabular data for classification and regression tasks
- **Use the RPT-1 Playground**: Explore the model interactively with example datasets to build an intuition for how it works
- **Prepare and upload data**: Format your own dataset as JSON and submit it to the model for inference
- **Interpret predictions**: Read and evaluate the model's output for both classification and regression scenarios

## What is RPT-1?

**SAP-RPT-1** — [SAP's Relational Pretrained Transformer model](https://www.sap.com/products/artificial-intelligence/sap-rpt.html) is a foundation model trained on structured data. It is available in Generative AI Hub to gain predictive insights from enterprise data. The model works by uploading example data rows as JSON and can do classification and regression predictions on your dataset.

## The RPT-1 Playground

👉 Familiarize yourself with the SAP-RPT-1 model by reading the paper: https://arxiv.org/pdf/2506.10707

👉 Open the [SAP-RPT-1 Playground](https://rpt.cloud.sap/). Use one of the example files from the playground to understand how the model works.

## The challenge

Now that you are familiar with SAP-RPT-1 and how to use the playground, we want to challenge you.
In the GitHub repository, you can find a CSV file [sales.csv](https://github.com/noravth/developer-challenge-042026/blob/main/sales.csv). This CSV file includes sales data for different types of products. The goal is to use SAP-RPT-1 to predict the missing values for some of these products. The model should predict the sales group respectively for the product type. If you run the prediction through SAP-RPT-1 you will see, initially, that it is hallucinating.

👉 Make sure you work with the SAP-RPT-1 model in a way that these predictions come out correct.

> You can use the SAP-RPT-1 Playground to upload the CSV and test your predictions and trainings.

To participate: Post which fields you have changed in order to make the predictions correct.
