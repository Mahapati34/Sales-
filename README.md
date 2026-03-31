# Sales-
A Sales Dashboard is a visual representation of sales data that helps track performance, monitor revenue, and analyze sales trends. It displays key metrics such as total sales, monthly revenue, top-selling products, and customer demand using charts and graphs. The dashboard helps businesses make data-driven decisions and improve sales strategies.
from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib import colors
from reportlab.lib.units import cm

doc = SimpleDocTemplate("sales_report.pdf", pagesize=A4,
                        rightMargin=2*cm, leftMargin=2*cm, topMargin=2*cm, bottomMargin=2*cm)

styles = getSampleStyleSheet()
story = []

# ── Title ──────────────────────────────────────────
title_style = ParagraphStyle('Title', parent=styles['Title'], fontSize=22,
                              textColor=colors.HexColor('#1a237e'), spaceAfter=6)
story.append(Paragraph("Sales Report - 2024", title_style))
story.append(Paragraph("Monthly Performance Overview", styles['Normal']))
story.append(Spacer(1, 0.5*cm))

# ── KPI Table ──────────────────────────────────────
heading_style = ParagraphStyle('Heading', parent=styles['Heading2'], fontSize=14,
                                textColor=colors.HexColor('#283593'), spaceBefore=12, spaceAfter=6)
story.append(Paragraph("Key Performance Indicators", heading_style))

kpi_data = [
    ["Metric",           "Target",        "Achieved",      "Status"],
    ["Total Revenue",    "Rs. 50,00,000", "Rs. 59,00,000", "Exceeded"],
    ["New Customers",    "500",           "612",           "Exceeded"],
    ["Avg Deal Size",    "Rs. 10,000",    "Rs. 9,640",     "Near Target"],
    ["Retention",        "85%",           "88%",           "Exceeded"],
    ["Sales Calls",      "2,000",         "1,850",         "Below Target"],
]

kpi_table = Table(kpi_data, colWidths=[4.5*cm, 3.5*cm, 3.5*cm, 3*cm])
kpi_table.setStyle(TableStyle([
    ('BACKGROUND',    (0,0), (-1,0),  colors.HexColor('#1a237e')),
    ('TEXTCOLOR',     (0,0), (-1,0),  colors.white),
    ('FONTNAME',      (0,0), (-1,0),  'Helvetica-Bold'),
    ('ALIGN',         (0,0), (-1,-1), 'CENTER'),
    ('ROWBACKGROUNDS',(0,1), (-1,-1), [colors.HexColor('#e8eaf6'), colors.white]),
    ('GRID',          (0,0), (-1,-1), 0.5, colors.grey),
    ('TOPPADDING',    (0,0), (-1,-1), 7),
    ('BOTTOMPADDING', (0,0), (-1,-1), 7),
]))
story.append(kpi_table)
story.append(Spacer(1, 0.5*cm))

# ── Monthly Sales Table ────────────────────────────
story.append(Paragraph("Monthly Sales Breakdown", heading_style))

monthly_data = [
    ["Month",     "Revenue (Rs.)", "Units", "Growth %"],
    ["January",   "4,20,000",      "420",   "+5%"],
    ["February",  "3,80,000",      "380",   "-9%"],
    ["March",     "4,90,000",      "490",   "+29%"],
    ["April",     "4,60,000",      "460",   "-6%"],
    ["May",       "5,10,000",      "510",   "+11%"],
    ["June",      "5,30,000",      "530",   "+4%"],
    ["July",      "5,80,000",      "580",   "+9%"],
    ["August",    "6,20,000",      "620",   "+7%"],
    ["September", "6,50,000",      "650",   "+5%"],
    ["October",   "5,90,000",      "590",   "-9%"],
    ["November",  "6,10,000",      "610",   "+3%"],
    ["December",  "6,60,000",      "660",   "+8%"],
    ["TOTAL",     "59,00,000",     "5,900", "+18%"],
]

monthly_table = Table(monthly_data, colWidths=[3.5*cm, 4.5*cm, 3.5*cm, 3*cm])
monthly_table.setStyle(TableStyle([
    ('BACKGROUND',    (0,0),  (-1,0),  colors.HexColor('#283593')),
    ('TEXTCOLOR',     (0,0),  (-1,0),  colors.white),
    ('FONTNAME',      (0,0),  (-1,0),  'Helvetica-Bold'),
    ('BACKGROUND',    (0,-1), (-1,-1), colors.HexColor('#1a237e')),
    ('TEXTCOLOR',     (0,-1), (-1,-1), colors.white),
    ('FONTNAME',      (0,-1), (-1,-1), 'Helvetica-Bold'),
    ('ALIGN',         (0,0),  (-1,-1), 'CENTER'),
    ('ROWBACKGROUNDS',(0,1),  (-1,-2), [colors.HexColor('#e8eaf6'), colors.white]),
    ('GRID',          (0,0),  (-1,-1), 0.5, colors.grey),
    ('TOPPADDING',    (0,0),  (-1,-1), 6),
    ('BOTTOMPADDING', (0,0),  (-1,-1), 6),
]))
story.append(monthly_table)
story.append(Spacer(1, 0.5*cm))

# ── Top Products Table ─────────────────────────────
story.append(Paragraph("Top Performing Products", heading_style))

prod_data = [
    ["Product",   "Revenue (Rs.)", "Units", "% of Total"],
    ["Product A", "18,00,000",     "1,800", "30.5%"],
    ["Product B", "14,50,000",     "1,450", "24.6%"],
    ["Product C", "11,20,000",     "1,120", "19.0%"],
    ["Product D", "8,80,000",      "880",   "14.9%"],
    ["Others",    "6,50,000",      "650",   "11.0%"],
]

prod_table = Table(prod_data, colWidths=[4*cm, 4*cm, 3.5*cm, 3*cm])
prod_table.setStyle(TableStyle([
    ('BACKGROUND',    (0,0), (-1,0),  colors.HexColor('#4a148c')),
    ('TEXTCOLOR',     (0,0), (-1,0),  colors.white),
    ('FONTNAME',      (0,0), (-1,0),  'Helvetica-Bold'),
    ('ALIGN',         (0,0), (-1,-1), 'CENTER'),
    ('ROWBACKGROUNDS',(0,1), (-1,-1), [colors.HexColor('#f3e5f5'), colors.white]),
    ('GRID',          (0,0), (-1,-1), 0.5, colors.grey),
    ('TOPPADDING',    (0,0), (-1,-1), 6),
    ('BOTTOMPADDING', (0,0), (-1,-1), 6),
]))
story.append(prod_table)
story.append(Spacer(1, 0.5*cm))

# ── Footer ─────────────────────────────────────────
footer_style = ParagraphStyle('Footer', parent=styles['Normal'], fontSize=9, textColor=colors.grey)
story.append(Paragraph("Generated on: March 31, 2026  |  Confidential", footer_style))

# ── Build PDF ──────────────────────────────────────
doc.build(story)
print("PDF ready: sales_report.pdf")
