# Product Requirements Document (PRD) - Prosty Deficyt

## 1. Product Overview

Prosty Deficyt is a personal web application for calorie tracking, designed with simplicity and motivation in mind through a streak and reward system. The application is built as an MVP targeting a single user, with a mobile-first responsive interface optimized for quick thumb-based interactions.

The core value proposition addresses the common problem of calorie counting being boring and easily abandoned. The app introduces gamification elements (streak counter, virtual shields) combined with a simplified interface to encourage consistent daily usage.

Key characteristics:
- Web application with responsive mobile-optimized design
- Backend powered by Supabase for authentication and data storage
- Cloud-synchronized data accessible from any device
- Completely free application (no monetization in MVP)
- Polish language interface with Polish product database
- Offline mode not required in MVP

## 2. User Problem

Counting calories is boring and easy to forget. Users lose data when changing phones or give up due to inconvenient and slow applications.

Primary pain points addressed:
- Tedious and time-consuming calorie logging process
- Lack of motivation to maintain consistency
- Data loss when switching devices
- Slow and complex existing applications
- No reward system for maintaining healthy habits

The target user is an individual seeking a simple, personal tool for daily calorie tracking without the complexity of social features, AI analysis, or barcode scanning. The user values speed, simplicity, and motivational elements over comprehensive nutritional analysis.

## 3. Functional Requirements

### 3.1 User Account System
- Email and password registration
- Email and password login
- Supabase-based authentication backend
- Cloud data synchronization
- Secure session management

### 3.2 Plan Generator (Onboarding)
- Input form with 5-6 fields: weight, height, age, gender, activity level
- BMR calculation using Mifflin-St Jeor formula
- Predefined calorie goals:
  - Light deficit: -250 kcal
  - Standard deficit: -500 kcal
  - Aggressive deficit: -750 kcal
  - Maintenance: 0 kcal
  - Light surplus: +250 kcal
  - Standard surplus: +500 kcal
  - Aggressive surplus: +750 kcal
- Daily calorie limit calculation and display

### 3.3 Meal Logging
- Product selection from database with quantity input
- Flexible unit system: pieces (szt), grams (g), milliliters (ml), portions (porcja)
- Unit converters with calorie mappings (e.g., 1 dumpling = 35g = 45 kcal)
- Flat list of daily entries (no mandatory meal categorization)
- Edit and delete entries from the last 7 days
- Read-only access to entries older than 7 days
- Day ends at midnight (00:00)
- No blocking when exceeding limit - visual warning only

### 3.4 Product Database
- Base database of 200-500 most popular Polish products
- User ability to add custom products
- Data storage: calories + macronutrients (protein, carbs, fat)
- Macronutrient display optional/hidden in MVP
- Default unit with converters per product

### 3.5 My Regular Meals (Favorites)
- Flat list of favorite products (no categorization)
- Support for single products
- Support for "recipes" (ingredient sets, e.g., "my oatmeal")
- One-click quick addition to daily log

### 3.6 Streak Counter
- Streak maintained when: at least 1 meal logged AND daily limit not exceeded by more than 10%
- Current streak length display
- Visual motivation elements
- Streak breaks when conditions not met

### 3.7 Virtual Shield System
- Reward: 1 shield earned for every 7 consecutive days of streak
- Maximum 3 shields in reserve
- Manual activation with confirmation prompt ("Do you want to use a Shield?")
- Shield protects streak for 1 day of limit exceeding
- Shield count display

### 3.8 Weight Tracking
- Daily manual weight input (morning)
- Visual reminder in application from 4:00 AM
- Weight trend chart over time
- Historical weight data storage

### 3.9 Charts and Reports
- Bar chart: daily calories vs limit (7/30 day view)
- Line chart: weight trend
- Key metrics display:
  - Average daily calories
  - Days within limit
  - Current streak length
  - Weight change (weekly)
- Average weekly deficit/surplus indicator

### 3.10 User Interface
- Responsive web application
- Mobile-first design optimization
- Large, thumb-friendly buttons
- Visual warning on limit exceeding (color change)
- Fast loading performance
- Readable on all phone screen sizes

### 3.11 Data Export
- Hidden/developer endpoint
- JSON or CSV format
- Export includes: calorie history, weight measurements
- Serves as data backup functionality

## 4. Product Boundaries

### In Scope (MVP)
- Email/password authentication via Supabase
- Calorie calculation using Mifflin-St Jeor formula
- Manual product entry with quantity
- Basic Polish product database (200-500 items)
- Custom product creation
- Favorite meals/recipes for quick logging
- Streak tracking with 10% tolerance
- Shield reward system (earn and use)
- Daily weight tracking with reminder
- Basic charts (calories, weight trend)
- Key statistics display
- 7-day edit window for entries
- Responsive mobile web interface
- Data export (JSON/CSV) as hidden feature

### Out of Scope (MVP)
- Barcode scanner - manual entry only
- Artificial Intelligence - no image analysis or AI-powered suggestions
- Social features - no friends, no public leaderboards
- Advanced notifications - no push reminders or notification system
- Offline mode - internet connection required
- Meal copying between days
- Automatic shield usage
- Meal categorization (breakfast, lunch, dinner)
- Multiple user profiles
- Premium/paid features
- Native mobile applications (iOS/Android)
- Integration with fitness devices or other apps
- Detailed macronutrient tracking display (stored but hidden)

### Unresolved Issues for Future Clarification
1. Product database source: Where to obtain the base of 200-500 Polish products with nutritional values
2. Weight reminder behavior: Should the visual reminder disappear after weight entry or remain visible until entry
3. Unit converter definitions: Who defines converters (e.g., 1 dumpling = 45 kcal) - predefined or user-defined when adding products
4. No-log day handling: What happens to streak when user logs no meals for an entire day (didn't exceed limit but didn't log either)
5. Weight validation: Should the app validate weight entry sensibility (e.g., warning for >2kg daily change)

## 5. User Stories

### Authentication and Account Management

US-001: User Registration
- ID: US-001
- Title: New user registration
- Description: As a new user, I want to register an account using my email and password so that I can securely store my calorie tracking data in the cloud.
- Acceptance Criteria:
  - User can access registration form from the landing page
  - Registration form requires email address and password
  - Password must meet minimum security requirements (minimum 8 characters)
  - System validates email format before submission
  - System checks for duplicate email addresses
  - Successful registration creates a new account in Supabase
  - User receives confirmation of successful registration
  - User is automatically logged in after registration
  - Invalid inputs display appropriate error messages

US-002: User Login
- ID: US-002
- Title: Existing user login
- Description: As a registered user, I want to log in with my email and password so that I can access my calorie tracking data from any device.
- Acceptance Criteria:
  - User can access login form from the landing page
  - Login form accepts email and password
  - Successful login redirects to main dashboard
  - Invalid credentials display appropriate error message
  - Session is maintained until explicit logout
  - User data is retrieved from cloud after login

US-003: User Logout
- ID: US-003
- Title: User logout
- Description: As a logged-in user, I want to log out of the application so that I can secure my account on shared devices.
- Acceptance Criteria:
  - Logout option is accessible from the main interface
  - Clicking logout ends the current session
  - User is redirected to login page after logout
  - User cannot access protected pages after logout

US-004: Password Recovery
- ID: US-004
- Title: Password reset
- Description: As a user who forgot my password, I want to reset it via email so that I can regain access to my account.
- Acceptance Criteria:
  - "Forgot password" link is available on login page
  - User can enter email address for password reset
  - System sends password reset email to valid registered addresses
  - Reset link in email allows setting a new password
  - New password must meet security requirements
  - User can log in with new password after reset

### Onboarding and Plan Generation

US-005: Profile Setup
- ID: US-005
- Title: Initial profile configuration
- Description: As a new user, I want to enter my physical data (weight, height, age, gender, activity level) so that the app can calculate my daily calorie limit.
- Acceptance Criteria:
  - Onboarding form appears after first registration
  - Form includes fields: current weight (kg), height (cm), age (years), gender (male/female), activity level (sedentary/light/moderate/active/very active)
  - All fields are required
  - Input validation prevents invalid data (negative numbers, unrealistic values)
  - Data is saved to user profile
  - Form cannot be skipped

US-006: Calorie Goal Selection
- ID: US-006
- Title: Select calorie goal
- Description: As a user completing onboarding, I want to select my calorie goal (deficit/maintenance/surplus) so that the app calculates my personalized daily limit.
- Acceptance Criteria:
  - Goal selection screen follows profile setup
  - Available options: light deficit (-250 kcal), standard deficit (-500 kcal), aggressive deficit (-750 kcal), maintenance, light surplus (+250 kcal), standard surplus (+500 kcal), aggressive surplus (+750 kcal)
  - Each option displays the calorie adjustment clearly
  - BMR is calculated using Mifflin-St Jeor formula
  - TDEE is calculated based on activity level
  - Daily limit = TDEE + selected goal adjustment
  - Final daily calorie limit is displayed and saved
  - User can proceed to main dashboard after selection

US-007: Profile Update
- ID: US-007
- Title: Update profile data
- Description: As a user, I want to update my physical data and calorie goal so that my daily limit reflects my current situation.
- Acceptance Criteria:
  - Settings/profile section is accessible from main interface
  - User can modify: weight, height, age, activity level, calorie goal
  - Changes trigger recalculation of daily limit
  - New limit takes effect immediately
  - Previous entries are not affected by limit changes

### Meal Logging

US-008: Search and Add Product
- ID: US-008
- Title: Add product from database
- Description: As a user, I want to search for a product in the database and add it to my daily log with a specific quantity so that I can track my calorie intake.
- Acceptance Criteria:
  - Search field is prominently displayed on main screen
  - Search returns matching products from database as user types
  - Product results show name and calories per default unit
  - User can select a product from search results
  - Quantity input appears after product selection
  - Default unit is pre-selected (szt, g, ml, or porcja)
  - User can change unit if multiple units are available
  - Calories are calculated based on quantity and unit
  - Submitting adds entry to today's log
  - Entry appears in daily list immediately

US-009: Add Custom Product
- ID: US-009
- Title: Create custom product
- Description: As a user, I want to add a product that doesn't exist in the database so that I can track foods not included in the base database.
- Acceptance Criteria:
  - "Add custom product" option is available when search yields no results
  - Custom product form includes: name, calories per 100g, default unit
  - Optional fields: protein, carbs, fat per 100g
  - User can define unit converters (e.g., 1 piece = 50g)
  - Custom product is saved to user's personal database
  - Custom product appears in future searches
  - Custom product can be added to daily log immediately after creation

US-010: View Daily Log
- ID: US-010
- Title: View today's meals
- Description: As a user, I want to see all products I've logged today with their calorie values so that I can track my daily intake.
- Acceptance Criteria:
  - Daily log is visible on main dashboard
  - Each entry shows: product name, quantity with unit, calories
  - Entries are displayed in a flat list (chronological order)
  - Running total of calories consumed is displayed
  - Remaining calories until daily limit is shown
  - Progress bar or indicator shows percentage of limit used

US-011: Edit Recent Entry
- ID: US-011
- Title: Edit meal entry
- Description: As a user, I want to edit a meal entry from the last 7 days so that I can correct mistakes in my logging.
- Acceptance Criteria:
  - Edit option is available for entries from the last 7 days
  - User can modify quantity and unit
  - User can change the product (replace with different product)
  - Calories are recalculated after edit
  - Daily totals are updated after edit
  - Changes are saved to database

US-012: Delete Entry
- ID: US-012
- Title: Remove meal entry
- Description: As a user, I want to delete a meal entry from the last 7 days so that I can remove incorrectly logged items.
- Acceptance Criteria:
  - Delete option is available for entries from the last 7 days
  - Confirmation prompt appears before deletion
  - Deleted entry is removed from daily log
  - Daily totals are recalculated after deletion
  - Deletion is permanent

US-013: View Historical Days
- ID: US-013
- Title: Browse past days
- Description: As a user, I want to view my meal logs from previous days so that I can review my eating history.
- Acceptance Criteria:
  - Navigation allows selecting previous dates
  - Historical day shows all logged entries
  - Daily total calories are displayed
  - Entries older than 7 days are read-only (no edit/delete)
  - Entries from last 7 days show edit/delete options
  - Current day is clearly indicated

### Favorite Meals

US-014: Add to Favorites
- ID: US-014
- Title: Save product as favorite
- Description: As a user, I want to save a product to my favorites so that I can quickly add it to future logs.
- Acceptance Criteria:
  - "Add to favorites" option is available when viewing a product
  - Product is added to favorites list with default quantity
  - User can set preferred quantity for the favorite
  - Favorite is saved to user's profile
  - Confirmation message appears after adding

US-015: Create Favorite Recipe
- ID: US-015
- Title: Create multi-item favorite
- Description: As a user, I want to create a "recipe" favorite consisting of multiple products so that I can log common meals quickly.
- Acceptance Criteria:
  - Option to create new recipe/combo favorite
  - User can add multiple products with quantities
  - Recipe has a custom name (e.g., "my oatmeal")
  - Total calories are calculated from all ingredients
  - Recipe is saved to favorites list
  - Recipe can be distinguished from single-product favorites

US-016: Quick Add from Favorites
- ID: US-016
- Title: One-click favorite logging
- Description: As a user, I want to add a favorite meal to my daily log with one click so that I can log regular meals in under 5 seconds.
- Acceptance Criteria:
  - Favorites section is easily accessible from main screen
  - Each favorite shows name and total calories
  - Tapping/clicking a favorite adds it to today's log immediately
  - For recipes, all component products are added as entries
  - Confirmation appears after adding
  - Daily totals update immediately

US-017: Manage Favorites
- ID: US-017
- Title: Edit and remove favorites
- Description: As a user, I want to edit or remove items from my favorites list so that I can keep it current with my eating habits.
- Acceptance Criteria:
  - Favorites management section is accessible
  - User can edit quantity/name of favorites
  - User can edit recipe ingredients and quantities
  - User can delete favorites
  - Deletion requires confirmation
  - Changes take effect immediately

### Streak System

US-018: View Current Streak
- ID: US-018
- Title: Display streak counter
- Description: As a user, I want to see my current streak count so that I am motivated to maintain my daily logging habit.
- Acceptance Criteria:
  - Streak counter is prominently displayed on main dashboard
  - Counter shows number of consecutive days
  - Streak is visually appealing and motivating
  - Counter updates in real-time as conditions are met

US-019: Streak Maintenance Check
- ID: US-019
- Title: Daily streak validation
- Description: As a user, I want the system to automatically check if I've maintained my streak conditions each day so that my streak is accurately tracked.
- Acceptance Criteria:
  - At day end (midnight), system evaluates streak conditions
  - Streak maintained if: at least 1 meal logged AND calories not exceeded by more than 10%
  - Streak counter increments if conditions met
  - Streak resets to 0 if conditions not met (and no shield used)
  - Historical streak data is preserved

US-020: Streak Break Warning
- ID: US-020
- Title: Streak at risk notification
- Description: As a user, I want to see a warning when my streak is at risk so that I can take action before losing my progress.
- Acceptance Criteria:
  - Warning appears if no meals logged for the day (evening hours)
  - Warning appears when approaching or exceeding limit
  - Warning is visually distinct (color, icon)
  - Warning indicates what action is needed
  - Warning includes shield usage option if available

### Shield System

US-021: Shield Accumulation
- ID: US-021
- Title: Earn shields
- Description: As a user, I want to earn a virtual shield for every 7 consecutive streak days so that I have protection against future slip-ups.
- Acceptance Criteria:
  - Shield is automatically awarded at day 7 of streak
  - Additional shields awarded at days 14, 21, etc.
  - Maximum 3 shields can be accumulated
  - Shield count is displayed on dashboard
  - Notification appears when shield is earned
  - Shields persist across sessions

US-022: View Shield Count
- ID: US-022
- Title: Display available shields
- Description: As a user, I want to see how many shields I have available so that I know my protection level.
- Acceptance Criteria:
  - Shield count displayed on main dashboard
  - Visual representation of shields (icons or counter)
  - Clear indication of maximum capacity (3)
  - Shield count is always accurate

US-023: Manual Shield Activation
- ID: US-023
- Title: Use shield to protect streak
- Description: As a user who has exceeded my daily limit, I want to be prompted to use a shield so that I can protect my streak.
- Acceptance Criteria:
  - Prompt appears when daily limit is exceeded by more than 10%
  - Prompt asks "Do you want to use a Shield?"
  - Prompt shows current shield count
  - User can accept (use shield) or decline
  - Using shield decrements shield count by 1
  - Using shield protects streak for that day
  - Declining means streak will be broken at day end
  - Shield can only be used once per day

US-024: Shield Protection Effect
- ID: US-024
- Title: Shield saves streak
- Description: As a user who used a shield, I want my streak to continue the next day so that my progress is preserved.
- Acceptance Criteria:
  - Day with shield usage is counted as valid streak day
  - Streak counter does not reset despite limit exceeded
  - Next day continues streak count normally
  - Shield usage is logged in history
  - No penalty for using shield

### Weight Tracking

US-025: Log Daily Weight
- ID: US-025
- Title: Enter morning weight
- Description: As a user, I want to log my weight each morning so that I can track my progress over time.
- Acceptance Criteria:
  - Weight input field is accessible from main dashboard
  - Input accepts decimal values (e.g., 75.5 kg)
  - Input validates reasonable weight range
  - Weight is saved with current date
  - Only one weight entry per day allowed
  - Existing entry can be updated same day
  - Confirmation appears after saving

US-026: Weight Entry Reminder
- ID: US-026
- Title: Visual weight reminder
- Description: As a user, I want to see a visual reminder to log my weight so that I don't forget this daily task.
- Acceptance Criteria:
  - Reminder appears from 4:00 AM onwards
  - Reminder is visually noticeable but not intrusive
  - Reminder indicates weight entry is pending
  - Reminder is visible until weight is entered (or end of day)

US-027: View Weight History
- ID: US-027
- Title: Browse weight records
- Description: As a user, I want to see my weight entries over time so that I can understand my progress.
- Acceptance Criteria:
  - Weight history is accessible from reports section
  - History shows date and weight for each entry
  - Entries are sorted chronologically (newest first or oldest first with option)
  - Missing days are handled gracefully (gaps shown or interpolated)

### Charts and Reports

US-028: Daily Calories Chart
- ID: US-028
- Title: View calorie history chart
- Description: As a user, I want to see a bar chart of my daily calories compared to my limit so that I can visualize my consistency.
- Acceptance Criteria:
  - Bar chart displays daily calorie intake
  - Daily limit is shown as reference line
  - Chart supports 7-day and 30-day views
  - Toggle between time periods is available
  - Days over limit are visually distinct (different color)
  - Days under limit show positive visual indication
  - Chart is responsive on mobile screens

US-029: Weight Trend Chart
- ID: US-029
- Title: View weight progress chart
- Description: As a user, I want to see a line chart of my weight over time so that I can track my body weight trend.
- Acceptance Criteria:
  - Line chart displays weight entries over time
  - Chart shows trend direction clearly
  - X-axis shows dates, Y-axis shows weight
  - Chart handles gaps in data (missing days)
  - Chart supports reasonable zoom/time range
  - Chart is responsive on mobile screens

US-030: Key Statistics Dashboard
- ID: US-030
- Title: View summary statistics
- Description: As a user, I want to see key statistics about my tracking so that I can quickly assess my performance.
- Acceptance Criteria:
  - Statistics section displays: average daily calories, number of days within limit, current streak length, weekly weight change
  - Average weekly deficit/surplus is calculated and shown
  - Statistics update in real-time as data changes
  - Time period for averages is clearly indicated
  - Statistics are easy to read on mobile

### Limit Warnings

US-031: Visual Limit Warning
- ID: US-031
- Title: Over-limit indicator
- Description: As a user approaching or exceeding my daily limit, I want clear visual feedback so that I am aware of my status.
- Acceptance Criteria:
  - Progress bar changes color when approaching limit (e.g., at 90%)
  - Progress bar shows distinct warning color when at limit
  - Progress bar shows alert color when over limit
  - Color changes are immediate as entries are added
  - Warning does not block adding more food
  - Numeric display shows calories over/under clearly

US-032: End of Day Limit Check
- ID: US-032
- Title: Daily limit evaluation
- Description: As a user, I want the system to evaluate my final daily intake at midnight so that my streak status is determined accurately.
- Acceptance Criteria:
  - At 00:00, system finalizes previous day's total
  - System checks if total exceeds limit by more than 10%
  - If within 10% tolerance, streak is maintained
  - If over 10%, streak break process initiates (shield prompt if available)
  - Evaluation results affect next day's streak display

### Data Export

US-033: Export Data
- ID: US-033
- Title: Download personal data
- Description: As a user, I want to export my tracking data so that I have a backup and can use the data elsewhere.
- Acceptance Criteria:
  - Export option is available (can be hidden/developer feature)
  - Export includes all calorie entries with dates
  - Export includes all weight measurements with dates
  - Export available in JSON format
  - Export available in CSV format
  - File downloads to user's device
  - Export includes all historical data

### Interface and Performance

US-034: Mobile Responsive Layout
- ID: US-034
- Title: Mobile-optimized interface
- Description: As a user on a smartphone, I want the interface to be fully responsive so that I can use the app comfortably with my thumb.
- Acceptance Criteria:
  - All interface elements scale appropriately on mobile screens
  - Buttons are large enough for thumb tapping (minimum 44x44 pixels)
  - Text is readable without zooming
  - No horizontal scrolling required
  - Forms are easy to fill on mobile
  - Touch targets have adequate spacing

US-035: Fast Loading
- ID: US-035
- Title: Quick application load
- Description: As a user, I want the application to load quickly so that I can log meals without delay.
- Acceptance Criteria:
  - Initial load completes in under 3 seconds on standard connection
  - Main dashboard is interactive quickly after load
  - Navigation between sections is instant
  - Adding meals provides immediate feedback
  - No noticeable lag during normal usage

US-036: Error Handling
- ID: US-036
- Title: Graceful error management
- Description: As a user, I want clear error messages when something goes wrong so that I understand what happened and what to do.
- Acceptance Criteria:
  - Network errors display user-friendly message
  - Form validation errors indicate specific fields
  - Failed saves prompt retry option
  - Errors do not crash the application
  - Recovery instructions are provided where applicable

US-037: Data Persistence
- ID: US-037
- Title: Cloud data synchronization
- Description: As a user, I want my data to be saved to the cloud so that I can access it from any device.
- Acceptance Criteria:
  - All entries are saved to Supabase backend
  - Saving happens automatically after each action
  - Data is available immediately on other devices after login
  - User does not need to manually save
  - Data persists across browser sessions

## 6. Success Metrics

### Performance Metrics

1. Load Time Performance
   - Target: Application loads and becomes interactive in under 3 seconds on 4G connection
   - Measurement: Time to First Contentful Paint and Time to Interactive
   - Frequency: Continuous monitoring

2. Interface Responsiveness
   - Target: Interface is fully usable and readable on all phone screen sizes (320px to 428px width)
   - Measurement: Manual testing on various device viewports
   - Frequency: Every release

3. Action Response Time
   - Target: Adding a meal from favorites completes in under 5 seconds (including user interaction)
   - Measurement: Time from tap to confirmation display
   - Frequency: User testing sessions

### Engagement Metrics

4. Streak Retention
   - Target: User maintains logging streak for minimum 14 consecutive days
   - Measurement: Maximum streak length achieved
   - Success threshold: User achieves 14+ day streak within first month

5. Daily Active Usage
   - Target: User logs at least one meal on 90% of days within a tracking period
   - Measurement: Days with entries / Total days since registration
   - Frequency: Weekly review

6. Weight Logging Consistency
   - Target: User logs weight on 80% of days
   - Measurement: Days with weight entry / Total days
   - Frequency: Weekly review

### Functional Metrics

7. Shield System Accuracy
   - Target: 100% accuracy in shield earning and usage calculations
   - Measurement: Shields earned after 7-day streaks, shields correctly deducted on use
   - Verification: Automated tests and manual verification

8. Calorie Calculation Accuracy
   - Target: 100% accuracy in daily calorie totals
   - Measurement: Sum of entry calories equals displayed total
   - Verification: Automated tests

9. Streak Calculation Accuracy
   - Target: 100% accuracy in streak maintenance logic
   - Measurement: Streak correctly maintained (within 10% limit) or broken (over 10% limit or no entries)
   - Verification: Automated tests with edge cases

### Data Integrity Metrics

10. Data Synchronization Reliability
    - Target: Zero data loss across sessions and devices
    - Measurement: All entries recoverable after logout/login
    - Verification: Regular backup verification

11. Export Data Completeness
    - Target: 100% of user data included in export
    - Measurement: Exported records match database records
    - Verification: Export validation tests
