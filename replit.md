# Nibras — Jordanian Renewable Energy Investment Platform

## Project Identity
**Nibras (نبراس)** is a solar land marketplace mobile app connecting landowners and energy developers in Jordan. Built with Expo/React Native.

## Tech Stack
- **Framework**: Expo SDK 54, Expo Router v6
- **Language**: TypeScript
- **UI**: React Native, react-native-svg, expo-linear-gradient
- **Navigation**: Expo Router (file-based, 5-tab layout)
- **Fonts**: Tajawal (Arabic), Inter (English)
- **i18n**: i18next + react-i18next (Arabic default, RTL)
- **Forms**: react-hook-form + zod
- **PDF**: expo-print + expo-sharing
- **Bottom sheets**: @gorhom/bottom-sheet

## User Roles
- **مالك أرض (Landowner)**: Submits parcels, receives offers
- **مطوّر طاقة (Developer)**: Browses parcels, submits offers — label is ALWAYS "Developer", never "Investor"
- **مدير (Admin)**: Manages platform, verifies parcels

## Design System
- **Background**: Midnight Navy `#0D1B2A`
- **Primary**: Deep Amber `#E8941A`
- **Accent**: Sky Blue `#3FA9D1`
- **Surface**: `#152538`

## Legal Foundation
References: Law No. 12/2024, Bylaw 58/2024, DLS Law No. 27/2024, Property Ownership Law No. 13/2019

### Rules Engine (services/legalRules.ts)
1. **Waqf Block** — permanently blocked, no action buttons, cannot be overridden
2. **State Amiri Reroute** — routes to MEMR government lease inquiry
3. **EMRC License Gate** — developer must have valid EMRC license to submit offers
4. **Foreign Developer Cabinet Approval** — Law No. 13/2019 requirement
5. **Grid Fee Calculator** — Buy-All/Sell-All: 0 JOD; Commercial on other mechanisms: 13 JOD/kWac/month
6. **Production Standards** — minimum 1,800 kWh/kWp/year irradiance, DC:AC limits per Bylaw 58/2024

## Project Structure
```
artifacts/nibras/
  app/
    _layout.tsx          # Root layout (fonts, RTL, auth routing)
    login.tsx            # Login screen (role selector, amber gradient)
    (tabs)/
      _layout.tsx        # 5-tab navigator
      index.tsx          # Map screen (GIS Phase 2 placeholder)
      parcels.tsx        # Parcel list/submission
      offers.tsx         # Deal flow
      advisor.tsx        # AI Advisor chat
      profile.tsx        # Profile + EMRC management
  types/
    legal.ts             # Full legal data types
    auth.ts              # User/Role types
  services/
    legalRules.ts        # All 6 legal rules + grid fee calculator
    mockApi.ts           # Mock backend (realistic delays, 6 mock parcels)
    contractTemplate.ts  # Bilingual HTML contract (DRAFT watermark)
  constants/
    theme.ts             # Design tokens (colors, spacing, typography)
    jordan.ts            # Governorates, irradiance zones, NEPCO grid lines
  locales/
    ar.ts                # Arabic translations (100% coverage)
    en.ts                # English translations
  context/
    AuthContext.tsx       # Auth state with AsyncStorage persistence
    I18nContext.tsx       # Language + RTL management
  hooks/
    useLegalRules.ts     # React hooks for rules engine
  components/
    NibrasLogo.tsx        # SVG logo (8-ray sun + ن letterform + sky blue dot)
    LegalWarning.tsx      # Reusable legal gate display component
```

## External APIs Required
| Service | Status | Where |
|---|---|---|
| Google Maps | Placeholder | app.json `GOOGLE_MAPS_API_KEY` |
| EMRC Verification | Mock (verifyEmrcLicense) | services/mockApi.ts |
| DLS Parcel DB | Mock | services/mockApi.ts |
| SignalR Real-Time | Mock (console.log stubs) | services/mockApi.ts |
| Push Notifications | Pending (Phase 6) | Not yet implemented |

## Implementation Status
- [x] Phase 0: Legal data types + rules engine (6 rules)
- [x] Phase 1: App shell, RTL, i18n, design tokens, NibrasLogo, auth, navigation
- [x] Phase 2: OSM map (CartoDB Dark + react-native-maps, no API key) + irradiance polygons + NEPCO polylines + 6 parcel markers
- [ ] Phase 3: Parcel submission wizard (4 steps)
- [ ] Phase 4: Deal flow + contract PDF generator (DRAFT watermark)
- [ ] Phase 5: AI Advisor (real LLM integration)
- [ ] Phase 6: Push notifications + SignalR
- [ ] Phase 7: Full profile screens + EMRC management

## Mock Data
6 demo parcels covering all land classifications:
- معان: Desert Zone, Buy-All/Sell-All, 2150 kWh/kWp/year (highest irradiance)
- العقبة: Private Tabu, Net Billing, 2050 kWh/kWp/year
- الزرقاء: Agricultural, Self-Consumption, 1920 kWh/kWp/year
- المفرق: Desert Zone, Buy-All/Sell-All, 2000 kWh/kWp/year
- إربد: Waqf (blocked), demonstrating Rule 1
- عمان: State Amiri, demonstrating Rule 2

## Legal Disclaimer
All contract PDFs are marked "DRAFT / NOT FOR LEGAL USE" prominently. They require review by a licensed Jordanian lawyer before production use.

## Pitch Deck (artifacts/nibras-pitch)
A 11-slide competition pitch deck built as a slides artifact at `/nibras-pitch/`.
- **Stack**: React + Tailwind CSS (Vite), Sora display font + Inter body
- **Design**: "Solar Authority" dark theme — navy #0D1B2A, amber #E8941A, sky blue #3FA9D1
- **Slides**: Cover, Intro, Problem, Solution, Market Opportunity, UVP, How It Works, Founders' Story, Team, Business Model, Closing CTA
- **Content**: Real Jordan data (Ma'an 6.3 kWh/kWp/day, 89K km², 31% target), real regulations (Bylaw 58/2024, Law 13/2019, EMRC, DLS, MEMR, NEPCO)
- Founders' Story and Team slides have placeholder cards with clear instructions for personalization
