# Migration `20201027031318`

This migration has been generated by Rinat at 10/27/2020, 6:13:18 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "public"."deals" DROP CONSTRAINT "deals_offerBidId_fkey"

CREATE TABLE "public"."_BidModelToDealModel" (
"A" text   NOT NULL ,
"B" text   NOT NULL 
)

CREATE UNIQUE INDEX "_BidModelToDealModel_AB_unique" ON "public"."_BidModelToDealModel"("A", "B")

CREATE INDEX "_BidModelToDealModel_B_index" ON "public"."_BidModelToDealModel"("B")

ALTER TABLE "public"."_BidModelToDealModel" ADD FOREIGN KEY ("A")REFERENCES "public"."bids"("id") ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE "public"."_BidModelToDealModel" ADD FOREIGN KEY ("B")REFERENCES "public"."deals"("id") ON DELETE CASCADE ON UPDATE CASCADE
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201027030736..20201027031318
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
@@ -97,10 +97,10 @@
   type BidType
   resourse Resourse
   coalMark CoalMark
   coalFraction CoalFraction
-  demandDeal DealModel 
-  offerDeals DealModel[] @relation("offer_bid_deals")
+  demandDeal DealModel @relation("myname")
+  offerDeals DealModel[] 
   creator UserModel @relation(fields: [creatorId], references: [id])
   location LocationModel @relation(fields: [locationId], references: [id])
   createdAt DateTime @default(now())
@@ -115,10 +115,10 @@
   demandBidId String
   offerBidId String
   matcherId String
-  demandBid BidModel @relation(fields: [demandBidId], references: [id])
-  offerBid BidModel @relation("offer_bid_deals", fields: [offerBidId], references: [id])
+  demandBid BidModel @relation("myname",fields: [demandBidId], references: [id])
+  offerBidz BidModel[] 
   matcher UserModel @relation(fields: [matcherId], references: [id])
   createdAt DateTime @default(now())
```


