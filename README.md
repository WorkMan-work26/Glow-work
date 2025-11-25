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

|**UPDATE 05-11-25**

checking internet connectivity to search perveance/state and District. if network is there then it allow user to search and edit text will be disabled, if no network then it will no allow user to search and edit text will be enabled.

|**UPDATE 06-11-25**

when online by searching we will get stateID and districtID but when manually entering it wont get stateID hence in validation checking state instde of stateID.

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

**WhiteGoodsVoucherDetailsFragment**
Displays vouchers in table using WhiteGoodsDetailsListAdapter.
Local table created for CRUD operations via T_GlosVoucherDetail.

**|UPDATE 28-10-25**

updated UI displaying total voucher amount, expected loan amount and cash expected below the table.

Add new voucher via top bar → navigates to WhiteGoodsVouchersDetailsEntryActivity.
Existing voucher loads read-only; new entry allows editing.
After save, updates local DB and navigates back to fragment.

**UPDATE 10-10-25**
Added Expected Loan Amount and Cash Expected below Total Voucher Amount as per FSD.
Expected Loan from T_GLOSClientLoan.get_glosClientLoan_branchwise.
Cash Expected based on FSD formula.

**UPDATE 14-10-25**
Logs printed only if debug mode enabled.

**WhiteGoodsVoucherDetailsEntryActivity**
After adding data, updates Temp_Member_Data_Sync with table name.

**|UPDATE 27-10-25**

changed total price entry time validation check with onSave validation.

**|UPDATE 05-11-25**

bug fixed -- when inserting new voucher detail initially it was checking voucher is already exist or not where i am not considering application file no. hence when single member if he add voucher data for another application file then generally it get data and display voucher is already exist. it was solved by checking based on application file no also in where condition.

**|UPDATE 10-11-25**
updated text view field name product code with quotation number in text view and code wherever required.

### T_GlosVoucherDetail
**UPDATE 13-10-25** 

– added deleteByBranchIdFileNo() used in InserUpdateTables class.
**UPDATE 14-10-25** 

– logs printed only if debug mode enabled.

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

**UPDATE 06-10-2025** 
– updated dropdowns with user codes.
**UPDATE 14-10-25**
– logs only if debug mode enabled, updates Temp_Member_Data_Sync.

**T_SeasonalWorkersDetails**

**UPDATE 13-10-25** – added deleteByBranchIdFileNo().
**UPDATE 14-10-25** – logs only if debug mode enabled.

---

**Weekly Business Cash Flow**
08-10-25 – Created new fragment and model T_WeeklyBusinessCashFlow.
Added table KEY_GLOS_WeeklyBusinessCashFlow.

**UPDATE 09-10-25** – Added info dialog to display business types and total income from T_GLOSBusinessDetail.
Added auto-calculations and try-catch blocks.

**UPDATE 14-10-25** – Logs only if debug mode enabled.
**UPDATE 15-10-25** – If no data, “No Data Found” displays.

**|UPDATE 10-11-25**
updated business other 1-6 text view ids


**T_WeeklyBusinessCashFlow**
UPDATE 13-10-25 – added deleteByBranchIdFileNo().
UPDATE 14-10-25 – logs only if debug mode enabled.
After adding data, updates Temp_Member_Data_Sync.

---

**Weekly Household Cash Flow**
09-10-25 – Created new fragment, model, DB class and table KEY_GLOS_WeeklyHousehodCashFlow.

10-10-2025 – Added sync for 4 screens:
Weekly Business Cash Flow, Weekly Household Cash Flow, White Goods, and Seasonal Workers.
Created checkForLocalDataSync, getLocalDataSync, updateLocalDataSync methods.

**UPDATE 14-10-25** – logs only if debug mode enabled.
After adding data, updates Temp_Member_Data_Sync.

**T_WeeklyHouseholdCashFlow**
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

**|UPDATE 30-10-25**

added insert method for 
t_GLOSOfflineClient
t_GLOSOfflineClientRelation
t_GLOSOfflineClientAddress
t_GLOSOfflineClientBankAccount

**|UPDATE 03-11-25**

added insert method for t_GLOSOfflineGroupMember

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


--------------------------------------------------------------------------------------------------------------------------------------------------------- 

###### **T_GLOSOfflineClient**

**27-10-25**

created kotlin class with insert, get and delete methods for new offline client table

KEY_GLOS_OFFLINE_Client_ApplicationFileNo

--------------------------------------------------------------------------------------------------------------------------------------------------------- 

###### **T_GLOSClientOfflineRelation**

**27-10-25**

created kotlin class with insert, get and delete methods for new offline client relation table

KEY_GLOS_OFFLINE_CLIENT_RELATION_ApplicationFileNo

--------------------------------------------------------------------------------------------------------------------------------------------------------- 

###### **T_GLOSClientOfflineBankAccount**

**27-10-25**

created kotlin class with insert, get and delete methods for new offline client bank account table

KEY_GLOSCLIENT_OFFLINE_BANK_ACCOUNT_ApplicationFileNo


--------------------------------------------------------------------------------------------------------------------------------------------------------- 

###### **T_GLOSClientOfflineAddress**

**27-10-25**

created kotlin class with insert, get and delete methods for new offline client address table

KEY_GLOS_OFFLINE_CLIENT_ADDRESS_ApplicationFileNo


--------------------------------------------------------------------------------------------------------------------------------------------------------- 

###### **BusinessDetailsActivity**

**27-10-25**

updated business date edit text with editText and date picker and related code logic in activity


--------------------------------------------------------------------------------------------------------------------------------------------------------- 

###### **CenterDetailsForm and CustomExpandableListAdapter**

**29-10-25**

when user select MY Files in Modules then in those list of files it need to show file download status for that i created one imageview and textview in xmls regarding that both class, if file is downloaded then it will display green color background file icon with File Downloaded text and if file is not downloaded then it will show red background with file icon with file not downloaded text programmatically in both of those classes.


getDownloadServerData_Response
callFileDownloadRequest --> call api and get client offline data insert into table


ImportMemberFragment
-when user click Drop/Import option this fragment will open.
-here when device is in offline it will display offline import
i.e importtypeid.equalsIgnoreCase("O") then it will navigate to OfflineClientListActivity

OfflineClientListActivity
ClientAdapter
-Here it will display all then clients name of selected file no. and branch with the help of ClientAdapter in recycler list.
-when user select any client name it will ask to import that client data or not if yes it will get selected all client data from T_GLOSOfflineClient and insert to T_GLOSClient and same as all offline data to its master tables.
-after importing it will navigate to CenterDetailStageForTesting.


**|UPDATE 03-11-25**

- added t_GLOSOfflineGroupMember import method.


T_GLOSOfflineGroupMember

- insert, get and delete methods for t_GLOSOfflineGroupMember table.



##### **ConsentActivity**

ProfileFragment(FAB C&C menu_consent) --> ConsentActivity(Certifiaction and Consent) --> SignatureMainLayout(Signature)
**06-11-25**
in signatureMainLayout user drawing signature and saving, after in ConsentActivity it was displaying in image view with 90' rotation -- updated it with no rotation.

##### **NomieeDetailsScreen**
**12-11-25**
some problem while adding nominee to relation, when adding nominee in check condition initially it was not checking memberType so when we add same nominee for other relation instead inserting it was always updating solved this issue by adding memberType in check method where condition.

**13-11-25**
 some changes in selection of nominee where when death benefit for Member then it will show Spouse same like that when death benefit for Spouse in that case it will display Member in selection dropdown.

**14-11-25**
while adding member as nominee for spouse there nomineeRelationShipRefNo for member is taking member id it was updating some spouse data for member, so instead of memberId hardcoding 0 value now it will update correctly.

##### **DeathBenefitForm**
**12-11-25**
initially for amount dropdown it was setting all amounts present in T_InsurencePremiumConfig table now updated with Death Benefit For dropdown selection, if it selected member then fetch only member amount or if selected Spouse it will fetch spouse amount list

##### **TrainingSessionEntryScreen**
**13-11-25**
here while saving need to add current time to db and sync so made those changes in application level later said to update time with date column, so updated changes for time was keep as it is and updated time to date field only, check with sync in xml parameter was passing correctly but in db it was storing default.

**17-11-25**

##### Training Session Changes

In training session for Training Session 5 need to add Booklet Issued switch in PresentAbsentAdapter and created isBookletIssued column in local db sending in sync and downloading in InsertUpdateTables.
also added session time in xml in TrainingSessionEntryScreen in sessionDoneDate passing session time with date in format and while displaying extracting that sessionDoneDate and setting text for Session date and Session Time, in TrainingSessionActivity added new time column to sessions table.

**18-11-25**

##### Training Session Changes

date and time in sessionDoneDate format issue checked with it and update where ever required. 

##### DropMemberList_Fragment

added some lines of code to delete newly added table date by ourBranchId, applicationFileNo, memberId.

##### LoanDetailsFragment

one check box text changes (Only Savings Required) and made one field disable, non mandatory, and isHide for loandetails_tv_disburesement.

**19-11-25**

##### PreparatoryActivitiesFragment

training sessions display date method added.

##### AddressForm and QDEAddressForm 
initially state, district were auto fill by pin code now removed pin code and added new dropdown Village Name from branchCodeDetails and displaying Village Name and Village Id, when network is connected it will call sp and get district, state details or if no network it allow user to enter district and state manually.  


**20-11-25**

##### AddressForm and QDEAddressForm 

checked with sp and binding data to views and checked with sync sp.

##### TrainingSessionActivity

added filter condition before passing attendanceList to adapter. here in Training Block 1 it will only display available sessions and for Training Block 2 it will display all the training sessions.

**24-11-25**

##### TrainingSessionEntryScreen

new functionality where for selection of each session if that client/member is existing and has restingTime then it will allow that member to those sessions in TrainingSessionConfig table, if new client it will allow to existing all sessions one by one.
for the above created new table TrainingSessionConfig with model class and operations class.

**25-11-25**

##### TrainingSessionEntryScreen

corrections in some logic, added new column restingTime in both online and offline client tables, also added in all related files, testing has been done working fine.
