# Google Ads API v21 -- Enum Reference (Integer-to-Name Mappings)

Source: Official protobuf definitions from `googleapis/googleapis` repository
URL: https://github.com/googleapis/googleapis/tree/master/google/ads/googleads/v21/enums

---

## 1. PositiveGeoTargetType
`campaign.geo_target_type_setting.positive_geo_target_type`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 5 | PRESENCE_OR_INTEREST |
| 6 | SEARCH_INTEREST |
| 7 | PRESENCE |

---

## 2. BiddingStrategyType
`campaign.bidding_strategy_type`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | ENHANCED_CPC |
| 3 | MANUAL_CPC |
| 4 | MANUAL_CPM |
| 5 | PAGE_ONE_PROMOTED |
| 6 | TARGET_CPA |
| 7 | TARGET_OUTRANK_SHARE |
| 8 | TARGET_ROAS |
| 9 | TARGET_SPEND |
| 10 | MAXIMIZE_CONVERSIONS |
| 11 | MAXIMIZE_CONVERSION_VALUE |
| 12 | PERCENT_CPC |
| 13 | MANUAL_CPV |
| 14 | TARGET_CPM |
| 15 | TARGET_IMPRESSION_SHARE |
| 16 | COMMISSION |
| 17 | INVALID |
| 18 | MANUAL_CPA |
| 19 | FIXED_CPM |
| 20 | TARGET_CPV |

---

## 3. CampaignStatus
`campaign.status`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | ENABLED |
| 3 | PAUSED |
| 4 | REMOVED |

---

## 4. AdGroupStatus
`ad_group.status`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | ENABLED |
| 3 | PAUSED |
| 4 | REMOVED |

---

## 5. KeywordMatchType
`ad_group_criterion.keyword.match_type`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | EXACT |
| 3 | PHRASE |
| 4 | BROAD |

---

## 6. DeviceType
`segments.device`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | MOBILE |
| 3 | TABLET |
| 4 | DESKTOP |
| 5 | OTHER |
| 6 | CONNECTED_TV |

---

## 7. CampaignPrimaryStatus
`campaign.primary_status`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | ELIGIBLE |
| 3 | PAUSED |
| 4 | REMOVED |
| 5 | ENDED |
| 6 | PENDING |
| 7 | MISCONFIGURED |
| 8 | LIMITED |
| 9 | LEARNING |
| 10 | NOT_ELIGIBLE |

---

## 8. CampaignPrimaryStatusReason
`campaign.primary_status_reasons`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | CAMPAIGN_REMOVED |
| 3 | CAMPAIGN_PAUSED |
| 4 | CAMPAIGN_PENDING |
| 5 | CAMPAIGN_ENDED |
| 6 | CAMPAIGN_DRAFT |
| 7 | BIDDING_STRATEGY_MISCONFIGURED |
| 8 | BIDDING_STRATEGY_LIMITED |
| 9 | BIDDING_STRATEGY_LEARNING |
| 10 | BIDDING_STRATEGY_CONSTRAINED |
| 11 | BUDGET_CONSTRAINED |
| 12 | BUDGET_MISCONFIGURED |
| 13 | SEARCH_VOLUME_LIMITED |
| 14 | AD_GROUPS_PAUSED |
| 15 | NO_AD_GROUPS |
| 16 | KEYWORDS_PAUSED |
| 17 | NO_KEYWORDS |
| 18 | AD_GROUP_ADS_PAUSED |
| 19 | NO_AD_GROUP_ADS |
| 20 | HAS_ADS_LIMITED_BY_POLICY |
| 21 | HAS_ADS_DISAPPROVED |
| 22 | MOST_ADS_UNDER_REVIEW |
| 23 | MISSING_LEAD_FORM_EXTENSION |
| 24 | MISSING_CALL_EXTENSION |
| 25 | LEAD_FORM_EXTENSION_UNDER_REVIEW |
| 26 | LEAD_FORM_EXTENSION_DISAPPROVED |
| 27 | CALL_EXTENSION_UNDER_REVIEW |
| 28 | CALL_EXTENSION_DISAPPROVED |
| 29 | NO_MOBILE_APPLICATION_AD_GROUP_CRITERIA |
| 30 | CAMPAIGN_GROUP_PAUSED |
| 31 | CAMPAIGN_GROUP_ALL_GROUP_BUDGETS_ENDED |
| 32 | APP_NOT_RELEASED |
| 33 | APP_PARTIALLY_RELEASED |
| 34 | HAS_ASSET_GROUPS_DISAPPROVED |
| 35 | HAS_ASSET_GROUPS_LIMITED_BY_POLICY |
| 36 | MOST_ASSET_GROUPS_UNDER_REVIEW |
| 37 | NO_ASSET_GROUPS |
| 38 | ASSET_GROUPS_PAUSED |
| 39 | MISSING_LOCATION_TARGETING |

---

## 9. AdGroupAdPrimaryStatus
`ad_group_ad.primary_status`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | ELIGIBLE |
| 3 | PAUSED |
| 4 | REMOVED |
| 5 | PENDING |
| 6 | LIMITED |
| 7 | NOT_ELIGIBLE |

---

## 10. AssetFieldType
`campaign_asset.field_type`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | HEADLINE |
| 3 | DESCRIPTION |
| 4 | MANDATORY_AD_TEXT |
| 5 | MARKETING_IMAGE |
| 6 | MEDIA_BUNDLE |
| 7 | YOUTUBE_VIDEO |
| 8 | BOOK_ON_GOOGLE |
| 9 | LEAD_FORM |
| 10 | PROMOTION |
| 11 | CALLOUT |
| 12 | STRUCTURED_SNIPPET |
| 13 | SITELINK |
| 14 | MOBILE_APP |
| 15 | HOTEL_CALLOUT |
| 16 | CALL |
| 17 | LONG_HEADLINE |
| 18 | BUSINESS_NAME |
| 19 | SQUARE_MARKETING_IMAGE |
| 20 | PORTRAIT_MARKETING_IMAGE |
| 21 | LOGO |
| 22 | LANDSCAPE_LOGO |
| 23 | VIDEO |
| 24 | PRICE |
| 25 | CALL_TO_ACTION_SELECTION |
| 26 | AD_IMAGE |
| 27 | BUSINESS_LOGO |
| 28 | HOTEL_PROPERTY |
| 30 | DEMAND_GEN_CAROUSEL_CARD |
| 31 | BUSINESS_MESSAGE |
| 32 | TALL_PORTRAIT_MARKETING_IMAGE |
| 33 | RELATED_YOUTUBE_VIDEOS |

Note: Integer 29 is skipped (reserved/unused).

---

## 11. ChangeEventResourceType
`change_event.change_resource_type`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | AD |
| 3 | AD_GROUP |
| 4 | AD_GROUP_CRITERION |
| 5 | CAMPAIGN |
| 6 | CAMPAIGN_BUDGET |
| 7 | AD_GROUP_BID_MODIFIER |
| 8 | CAMPAIGN_CRITERION |
| 9 | FEED |
| 10 | FEED_ITEM |
| 11 | CAMPAIGN_FEED |
| 12 | AD_GROUP_FEED |
| 13 | AD_GROUP_AD |
| 14 | ASSET |
| 15 | CUSTOMER_ASSET |
| 16 | CAMPAIGN_ASSET |
| 17 | AD_GROUP_ASSET |
| 18 | ASSET_SET |
| 19 | ASSET_SET_ASSET |
| 20 | CAMPAIGN_ASSET_SET |

---

## 12. ResourceChangeOperation
`change_event.resource_change_operation`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | CREATE |
| 3 | UPDATE |
| 4 | REMOVE |

---

## 13. ConversionActionCategory
`conversion_action.category`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | DEFAULT |
| 3 | PAGE_VIEW |
| 4 | PURCHASE |
| 5 | SIGNUP |
| 7 | DOWNLOAD |
| 8 | ADD_TO_CART |
| 9 | BEGIN_CHECKOUT |
| 10 | SUBSCRIBE_PAID |
| 11 | PHONE_CALL_LEAD |
| 12 | IMPORTED_LEAD |
| 13 | SUBMIT_LEAD_FORM |
| 14 | BOOK_APPOINTMENT |
| 15 | REQUEST_QUOTE |
| 16 | GET_DIRECTIONS |
| 17 | OUTBOUND_CLICK |
| 18 | CONTACT |
| 19 | ENGAGEMENT |
| 20 | STORE_VISIT |
| 21 | STORE_SALE |
| 22 | QUALIFIED_LEAD |
| 23 | CONVERTED_LEAD |

Note: Integer 6 is skipped (reserved/unused).

---

## 14. ConversionActionCountingType
`conversion_action.counting_type`

| Integer | Name |
|---------|------|
| 0 | UNSPECIFIED |
| 1 | UNKNOWN |
| 2 | ONE_PER_CLICK |
| 3 | MANY_PER_CLICK |
