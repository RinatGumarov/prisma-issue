# Migration `20201027030417`

This migration has been generated by Rinat at 10/27/2020, 6:04:17 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql

```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201027020055-rename-and-restructure-deals..20201027030417
--- datamodel.dml
+++ datamodel.dml
@@ -3,9 +3,9 @@
 }
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url = "***"
 }
 enum Role {
   BUYER
@@ -97,9 +97,9 @@
   type BidType
   resourse Resourse
   coalMark CoalMark
   coalFraction CoalFraction
-  demandDeal DealModel  @relation("demand_bid_deals")
+  demandDeal DealModel 
   offerDeals DealModel[] @relation("offer_bid_deals")
   creator UserModel @relation(fields: [creatorId], references: [id])
   location LocationModel @relation(fields: [locationId], references: [id])
@@ -115,9 +115,9 @@
   demandBidId String
   offerBidId String
   matcherId String
-  demandBid BidModel @relation("demand_bid_deals", fields: [demandBidId], references: [id])
+  demandBid BidModel @relation(fields: [demandBidId], references: [id])
   offerBid BidModel @relation("offer_bid_deals", fields: [offerBidId], references: [id])
   matcher UserModel @relation(fields: [matcherId], references: [id])
   createdAt DateTime @default(now())
```


