# Glow-work
---

## **Village Survey Changes made**

These all fragments will come under villageSurvay_SwipeTabActivity

As per FSD document some fields which are need to remove made them non-mandatory, disabled and invisible.

---

**1. VillageSurvey_VillageDetailsFragment**

Sub Dist is need to remove but when we want to search village, sub dist would not be empty.
So on click of search village name, the if-condition validating sub dist was commented.
**UPDATE**
**16-10-25**
updated village name replaced search by dropdown 

---

**2. Village Category**
While adding new village category according to FSD, population must be valid by percentage.
Both men and women % should not exceed 100%. The remaining population will be calculated dynamically based on entered values.

---

**3. Village Boundaries**
New drop down added.
While adding village boundaries, existing field was an edit text. According to FSD, need to replace village name edit text with a drop down.
Removed edit text visibility, added a new drop down with the same label “Village Name”.
Replaced edit text getText with spinner selected value.

06-10-2025
Village name drop down is getting names from BranchCode_Detail by BranchId.

In VillageSurvey_VillageBoundriesFragment, previously the village name displayed from local DB directly.
Now it uses dropdown. When fetching the same village name, it stores village sub code id and displays it accordingly.
In method t_villageSurvey_villageBoundaries.villageSurvey_Boundaries_getAllRecordsWithHeading(), BranchCode_Detail DB class is passed to get description with key and insert that into the list to display in the table.

---

**4. Basis Information**
New fields: 3 edit texts and 3 drop downs.

06-10-2025
New fields were updated with sync method in all places.

---

**5. Law and Order Scenario**
Trending → new drop down added.

06-10-2025
New fields were updated with sync method in all places.
Trending drop down values come from userCoder by ID TrendingId.

07-10-2025
While updating law and order details, it was updating based on violenceID which was empty, so not updating.
In T_VillageSurvey_LowOrderScenario.Update_INTO__LowOrderScenario(), commented violenceId — now updates successfully.

08-10-25
Enabled violence type and added in userCode.
New fields now add with violence type and update based on that.
Uncommented violenceId in update method.

Initially, law and order table updates were based on casteViolenceId — now changed to violenceType.
User can add only 2 entries.

Displaying new field “Trending” in VillageSurvey_LowOrderScenarioActivityFragment table.
Data fetched dynamically from VillageSurvey_SqliteAdapter.
Earlier had a condition `if(length > 2){ length = 3; }` which limited columns — now commented, so all items display.

Trending dropdown ID now displays description fetched via T_UserCodeDetails in
villageSurvey_LowOrderScenario_getAllRecordsWithHeading().

---

**6. Financial Infrastructure**
Updated dropdown with new edit text.
Made existing spinner visibility gone to avoid validation issues.
Created new edit text, passing user input value in place of dropdown.

---

**White Goods Vouchers Details**
Created new fragment:
Member Files → Group Details → Application → Profile Details → User Level → Bank

WhiteGoodsVoucherDetailsFragment
Displays vouchers in table using WhiteGoodsDetailsListAdapter.
Local table created for CRUD operations via T_GlosVoucherDetail.

Add new voucher via top bar → navigates to WhiteGoodsVouchersDetailsEntryActivity.
Existing voucher loads read-only; new entry allows editing.
After save, updates local DB and navigates back to fragment.

UPDATE 10-10-25
Added Expected Loan Amount and Cash Expected below Total Voucher Amount as per FSD.
Expected Loan from T_GLOSClientLoan.get_glosClientLoan_branchwise.
Cash Expected based on FSD formula.

UPDATE 14-10-25
Logs printed only if debug mode enabled.

WhiteGoodsVoucherDetailsEntryActivity
After adding data, updates Temp_Member_Data_Sync with table name.

T_GlosVoucherDetail
UPDATE 13-10-25 – added deleteByBranchIdFileNo() used in InserUpdateTables class.
UPDATE 14-10-25 – logs printed only if debug mode enabled.

---

**Seasonal Workers Details Fragment**
Path not decided yet.
Created form with fields:

* IF REPEAT, NUMBER OF TIMES WORKED FOR OVERSEAS EMPLOYER(S)
* TEAM LEADER FULL NAME
* TEAM LEADER PHONE NUMBER
* TEAM LEADER EMAIL / SOCIAL MEDIA ACCOUNT
* NUMBER OF TEAM MEMBERS
* NAME OF EMPLOYER (COMPANY)
* COUNTRY OF EMPLOYMENT (dropdown)
* EMPLOYER TELEPHONE
* EMPLOYER EMAIL
* CONTRACT DURATION / TERM
* SALARY FREQUENCY (Dropdown – Weekly/Monthly)
* NET PAY AMOUNT
* REJECTED FROM SEASONAL WORK BEFORE? (Yes/No)
* ANY RELATIVES IN THE PROGRAM? (Yes/No)
* IF YES, NAME MEMBER AND RELATION (Conditional Mandatory)

When user clicks Save → updates to local DB.

UPDATE 06-10-2025 – updated dropdowns with user codes.
UPDATE 14-10-25 – logs only if debug mode enabled, updates Temp_Member_Data_Sync.

T_SeasonalWorkersDetails
UPDATE 13-10-25 – added deleteByBranchIdFileNo().
UPDATE 14-10-25 – logs only if debug mode enabled.

---

**Weekly Business Cash Flow**
08-10-25 – Created new fragment and model T_WeeklyBusinessCashFlow.
Added table KEY_GLOS_WeeklyBusinessCashFlow.

UPDATE 09-10-25 – Added info dialog to display business types and total income from T_GLOSBusinessDetail.
Added auto-calculations and try-catch blocks.

UPDATE 14-10-25 – Logs only if debug mode enabled.
UPDATE 15-10-25 – If no data, “No Data Found” displays.

T_WeeklyBusinessCashFlow
UPDATE 13-10-25 – added deleteByBranchIdFileNo().
UPDATE 14-10-25 – logs only if debug mode enabled.
After adding data, updates Temp_Member_Data_Sync.

---

**Weekly Household Cash Flow**
09-10-25 – Created new fragment, model, DB class and table KEY_GLOS_WeeklyHousehodCashFlow.

10-10-2025 – Added sync for 4 screens:
Weekly Business Cash Flow, Weekly Household Cash Flow, White Goods, and Seasonal Workers.
Created checkForLocalDataSync, getLocalDataSync, updateLocalDataSync methods.

UPDATE 14-10-25 – logs only if debug mode enabled.
After adding data, updates Temp_Member_Data_Sync.

T_WeeklyHouseholdCashFlow
UPDATE 13-10-25 – added deleteByBranchIdFileNo().
UPDATE 14-10-25 – logs only if debug mode enabled.

---

**Business Details Entry Screen**
**UPDATE - 16-10-25**
updated xml edit text fields which only required numbers

---

**HomeActivity, MainMenuForm, GlosDataSyncNew, GLOSManualSync, ModuleFragment**
Added sync flow up to step 5.

UPDATE 13-10-2025 – Renamed parameters:
IngredientsRawMaterials → IngRawMaterial
OtherFamilyMemberIncome → OtherFamilyMemIncome
IncomeOther1 → OtherIncome1
IncomeOther2 → OtherIncome2
IncomeOther3 → OtherIncome3
ExpenseOther1 → OtherExpense1
ExpenseOther2 → OtherExpense2
ExpenseOther3 → OtherExpense3
TL_FullName → TLName
TL_PhoneNo → TLPhoneNumber
TL_Mail → TLEmailOrMediaAcc
NoOfTeamMembers → NoOfTeamMemberCompany
NameOfEmployer → NameOfCompany
WorkCountry → CountryofEmployment
SalaryFrequency → SalaryFrequency
NetPayAmount → NetPaySalary
PreviousRejection → RejectedWorkBeforeID
AnyRelatives → Relav
TotalPrice → TotalAmount

UPDATE 14-10-25 – added Loan Proposal sync method.

**|UPDATE 17-10-25**

in business sync one field is mismatched getTargetWeeklyIncome is passing place of getTargetWeeklySalesStr corrected it 

---

**InsertUpdateTables**
Added new nodes:
t_GlosVoucherDtls, t_GlosSeasonalWorkersDtls, t_GLOSWeeklyBusinessCashFlow, t_GLOSWeeklyHouseholdCashFlow
inside downloadFileDetails() to fetch cloud data and insert/update local DB.

UPDATE 14-10-25 – logs only if debug mode enabled.
Added loan proposal and business details download methods.

**|UPDATE 17-10-25**

added death benefit,nominee details, central approval justification, contact person details, GLOSSessionAttendance download file details.

---

**SqlitDataClass**
14-10-25 – Added new tables to tablenameList:
KEY_GLOS_VoucherDetail
KEY_GLOS_SeasonalWorkersDetail
KEY_GLOS_WeeklyBusinessCashFlow
KEY_GLOS_WeeklyHouseholdCashFlow
LoanProposal

**|UPDATE 24-10-25**

added newly created 4 offline client tables to tablenameList 

---

**MDESwipeTabActivity**
14-10-25 – Added navigation for 6 new fragments.

---

**ApplicationStatusAdapter**
14-10-25 – Added status update methods for newly created 6 screens.

**23-10-2025**

updated death benefit application status update here i just comment the tab_insurance existing and added death benefit in all required places. in string xml file removed Insurance and added Death Benefit in memberdataenterlist.

---

**MDE**
15-10-25 – Added isMandatory and isEnabled checks for new screens.

---

###### **GLOS_DataSource**

**24-10-25**

added new 4 client tables 
t_GLOSOfflineClient
t_GLOSOfflineClientRelation
t_GLOSOfflineClientAddress
t_GLOSOfflineClientBankAccount

