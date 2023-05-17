---
parser: v2
primary_tag: programming-tool>abap-extensibility
tags: [ tutorial>beginner, products>sap-hana\,-express-edition ]
time: 5
---

# Introduction to Set Keyboard and Time Zone Test Green2 upd 222
<!-- description --> The VM defaults to an English (US) QWERTY keyboard, and the UTC time zone. When prompted, change the keyboard layout and time zone to match your location, or accept the defaults.

<!-- loiod0775daa77ca4aaea29ea74b3e2e2ac1 -->

## Prerequisites
 - **Tutorials:**  You have completed [Import the OVA](hxe-ua-ova-vm) 

## You will learn
You'll learn how to start the VM, change the VM default keyboard layout, and change the default time zone.

---

### Introduction Start your VM updated


Open your hypervisor application.

Power on (or click *Play* on) your SAP HANA 2.0, express edition VM.

<!-- size:150px -->![icon1](icon1.png) 

![icon2](icon2.png)

![hxe2_vm_start_0](hxe2_vm_start_0.png)


### Introduce Change the keyboard layout if your laptop doesn't use an English (US) keyboard

<!-- size:100px --> ![drivers](sign-check-icon.png) <iframe width="560" height="315" src=https://www.youtube.com/embed/do_UT5NqAO0 frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> 

The system prompts you to either change the VM keyboard, or accept the default English (US) QWERTY keyboard. Enter `Y` to change the keyboard or `N` to use the default.

> Note:
> Having difficulty entering text in your virtual machine in `VMWare`? Press ` CTRL G ` to switch the focus from your host machine to the VM.
> 
> 

![HXE_change_keyboard_prompt_5](HXE_change_keyboard_prompt_5.png)

If you opt to change the keyboard, the System Keyboard Configuration page displays.

![HXE_change_keyboard_GUI_PNG_1](HXE_change_keyboard_GUI_PNG_1.png)

```Shell (Microsoft Windows)
mkdir %HOMEPATH%\HANAClientsTutorial\nodeX509OpenSSL
cd %HOMEPATH%\HANAClientsTutorial\nodeX509OpenSSL
```

```Shell (Linux or macOS)
mkdir $HOME/HANAClientsTutorial/nodeX509OpenSSL
cd $HOME/HANAClientsTutorial/nodeX509OpenSSL
```

Use the arrow keys to scroll to the desired keyboard layout. `Tab` to the *OK* button, or press `F10`, to save your changes. A message displays while the system processes the keyboard layout change.

![HXE_change_keyboard_process_PNG_2](HXE_change_keyboard_process_PNG_2.png) 


### Introduction Change time zone


Change the time zone if your laptop is not in the default UTC (GMT) time zone.

Enter `Y` to change the time zone, or `N` to accept the default.

![HXE_change_timezone_PNG_4](HXE_change_timezone_PNG_4.png)

If you opt to change the timezone, the Clock and Time Zone page displays.

![HXE_change_timezone_GUI_3](HXE_change_timezone_GUI_3.png)

In the Region pane, use the arrow keys to scroll down to the correct region. `Tab` to the Time Zone pane and select the correct time zone. `Tab` to the *OK* button, or press `F10`, to save your changes.

### Connect with the Interactive SQL Client (DBISQL)


The data lake client install includes [dbisql Interactive SQL Utility](https://urldefense.com/v3/__https://help.sap.com/docs/SAP_HANA_DATA_LAKE/a895964984f210158925ce02750eb580/a373b67884f21015a722c2c0a58b94ad.html__;!!GF_29dbcQIUBPA!3-VGFthfLzox1V6QHvLyMpJH64RtcqU-Eouowl25Y9BFMo6d1FKf_CKiAj8866Ac9_PtxCoS_TAavxoj14F20HYN$ [help[.]sap[.]com]), which can be used to connect and query a data lake Relational Engine. The following steps will provide instructions on how to connect to the data lake Relational Engine using DBISQL and then populate the previously created tables with sample data.

1. Start the GUI version of DBISQL from the Microsoft Windows Start menu, by browsing to it under SAP > Interactive SQL and double clicking on it, or by entering `dbisql` in a terminal.

    ![start dbisql](dbisql-start-1.png)

2. Specify the connection type.

    ![Connection type](dbisql-connection-type.png)

    >The Connect window may appear enlarged on the screen. This can be adjusted by lowering the Scale and layout value in the device display settings.

3. Provide the connection details. See below on how to obtain the instance ID and landscape values.

    ![instance ID and landscape](connect-to-dl-iq.png)

    >SAP HANA Cloud Central can be used to get the instance ID and landscape value.  The landscape value can be obtained from the SQL Endpoint by removing the instance ID from the start and port number from the end.

    >![copy sql endpoint](dbisql-copy-endpoint.png)
    >
    > A failure to connect could be caused by the allowed connections list, which is editable in SAP HANA Cloud Central.  

    ![DBISQL Connected](dbisql-connection-type.png)

    >DBISQL can also be started without a GUI.
    >
    >```Shell (Windows)
    dbisql -c "uid=USER1;pwd=Password1;host=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.iq.hdl.xxxx-xxxx.hanacloud.ondemand.com:443;ENC=TLS(tls_type=rsa;direct=yes)" -nogui
    >```
    >
    >In a Bash shell, strings in double quotes versus single quotes are treated [differently](https://urldefense.com/v3/__https://stackoverflow.com/questions/6697753/difference-between-single-and-double-quotes-in-bash__;!!GF_29dbcQIUBPA!3-VGFthfLzox1V6QHvLyMpJH64RtcqU-Eouowl25Y9BFMo6d1FKf_CKiAj8866Ac9_PtxCoS_TAavxoj14XmWtKD$ [stackoverflow[.]com]).
    >
    >```Shell (Linux)
    dbisql -c 'uid=USER1;pwd=Password1;host=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.iq.hdl.trial-XXXX.hanacloud.ondemand.com:443;ENC=TLS(tls_type=rsa;direct=yes)' -nogui
    >```

    >![DBISQL connected nogui](hxe2_vm_start_0.png)


### Insert data with Interactive SQL Client (DBISQL)


1. Execute the following insert statements to provide some sample data.

    >If you do not wish to use the GUI mode, paste the insert statements into a file first and then run `dbisql -c "uid..." sql.sql`.

    ```SQL
    SET SCHEMA HOTEL;
    INSERT INTO HOTEL VALUES(10, 'Congress', '155 Beechwood St.', 'Seattle', 'WA', '20005');
    INSERT INTO HOTEL VALUES(11, 'Regency', '477 17th Avenue', 'Seattle', 'WA', '20037');
    INSERT INTO HOTEL VALUES(12, 'Long Island', '1499 Grove Street', 'Long Island', 'NY', '11788');
    INSERT INTO HOTEL VALUES(13, 'Empire State', '65 Yellowstone Dr.', 'Albany', 'NY', '12203');
    INSERT INTO HOTEL VALUES(14, 'Midtown', '12 Barnard St.', 'New York', 'NY', '10019');
    INSERT INTO HOTEL VALUES(15, 'Eighth Avenue', '112 8th Avenue', 'New York', 'NY', '10019');
    INSERT INTO HOTEL VALUES(16, 'Lake Michigan', '354 OAK Terrace', 'Chicago', 'IL', '60601');
    INSERT INTO HOTEL VALUES(17, 'Airport', '650 C Parkway', 'Rosemont', 'IL', '60018');
    INSERT INTO HOTEL VALUES(18, 'Sunshine', '200 Yellowstone Dr.', 'Clearwater', 'FL', '33575');
    INSERT INTO HOTEL VALUES(19, 'Beach', '1980 34th St.', 'Daytona Beach', 'FL', '32018');
    INSERT INTO HOTEL VALUES(20, 'Atlantic', '111 78th St.', 'Deerfield Beach', 'FL', '33441');
    INSERT INTO HOTEL VALUES(21, 'Long Beach', '35 Broadway', 'Long Beach', 'CA', '90804');
    INSERT INTO HOTEL VALUES(22, 'Indian Horse', '16 MAIN STREET', 'Palm Springs', 'CA', '92262');
    INSERT INTO HOTEL VALUES(23, 'Star', '13 Beechwood Place', 'Hollywood', 'CA', '90029');
    INSERT INTO HOTEL VALUES(24, 'River Boat', '788 MAIN STREET', 'New Orleans', 'LA', '70112');
    INSERT INTO HOTEL VALUES(25, 'Ocean Star', '45 Pacific Avenue', 'Atlantic City', 'NJ', '08401');
    INSERT INTO HOTEL VALUES(26, 'Bella Ciente', '1407 Marshall Ave', 'Longview', 'TX', '75601');

    INSERT INTO ROOM VALUES(10, 'single', 20, 135.00);
    INSERT INTO ROOM VALUES(10, 'double', 45, 200.00);
    INSERT INTO ROOM VALUES(12, 'single', 10, 70.00);
    INSERT INTO ROOM VALUES(12, 'double', 13, 100.00);
    INSERT INTO ROOM VALUES(13, 'single', 12, 45.00);
    INSERT INTO ROOM VALUES(13, 'double', 15, 80.00);
    INSERT INTO ROOM VALUES(14, 'single', 20, 85.00);
    INSERT INTO ROOM VALUES(14, 'double', 35, 140.00);
    INSERT INTO ROOM VALUES(15, 'single', 50, 105.00);
    INSERT INTO ROOM VALUES(15, 'double', 230, 180.00);
    INSERT INTO ROOM VALUES(15, 'suite', 12, 500.00);
    INSERT INTO ROOM VALUES(16, 'single', 10, 120.00);
    INSERT INTO ROOM VALUES(16, 'double', 39, 200.00);
    INSERT INTO ROOM VALUES(16, 'suite', 20, 500.00);
    INSERT INTO ROOM VALUES(17, 'single', 4, 115.00);
    INSERT INTO ROOM VALUES(17, 'double', 11, 180.00);
    INSERT INTO ROOM VALUES(18, 'single', 15, 90.00);
    INSERT INTO ROOM VALUES(18, 'double', 19, 150.00);
    INSERT INTO ROOM VALUES(18, 'suite', 5, 400.00);
    INSERT INTO ROOM VALUES(19, 'single', 45, 90.00);
    INSERT INTO ROOM VALUES(19, 'double', 145, 150.00);
    INSERT INTO ROOM VALUES(19, 'suite', 60, 300.00);
    INSERT INTO ROOM VALUES(20, 'single', 11, 60.00);
    INSERT INTO ROOM VALUES(20, 'double', 24, 100.00);
    INSERT INTO ROOM VALUES(21, 'single', 2, 70.00);
    INSERT INTO ROOM VALUES(21, 'double', 10, 130.00);
    INSERT INTO ROOM VALUES(22, 'single', 34, 80.00);
    INSERT INTO ROOM VALUES(22, 'double', 78, 140.00);
    INSERT INTO ROOM VALUES(22, 'suite', 55, 350.00);
    INSERT INTO ROOM VALUES(23, 'single', 89, 160.00);
    INSERT INTO ROOM VALUES(23, 'double', 300, 270.00);
    INSERT INTO ROOM VALUES(23, 'suite', 100, 700.00);
    INSERT INTO ROOM VALUES(24, 'single', 10, 125.00);
    INSERT INTO ROOM VALUES(24, 'double', 9, 200.00);
    INSERT INTO ROOM VALUES(24, 'suite', 78, 600.00);
    INSERT INTO ROOM VALUES(25, 'single', 44, 100.00);
    INSERT INTO ROOM VALUES(25, 'double', 115, 190.00);
    INSERT INTO ROOM VALUES(25, 'suite', 6, 450.00);

    INSERT INTO CUSTOMER VALUES(1000, 'Mrs', 'Jenny', 'Porter', '1340 N. Ash Street, #3', '10580');
    INSERT INTO CUSTOMER VALUES(1001, 'Mr', 'Peter', 'Brown', '1001 34th St., APT.3', '48226');
    INSERT INTO CUSTOMER VALUES(1002, 'Company', NULL, 'Datasoft', '486 Maple St.', '90018');
    INSERT INTO CUSTOMER VALUES(1003, 'Mrs', 'Rose', 'Brian', '500 Yellowstone Drive, #2', '75243');
    INSERT INTO CUSTOMER VALUES(1004, 'Mrs', 'Mary', 'Griffith', '3401 Elder Lane', '20005');
    INSERT INTO CUSTOMER VALUES(1005, 'Mr', 'Martin', 'Randolph', '340 MAIN STREET, #7', '60615');
    INSERT INTO CUSTOMER VALUES(1006, 'Mrs', 'Sally', 'Smith', '250 Curtis Street', '75243');
    INSERT INTO CUSTOMER VALUES(1007, 'Mr', 'Mike', 'Jackson', '133 BROADWAY APT. 1', '45211');
    INSERT INTO CUSTOMER VALUES(1008, 'Mrs', 'Rita', 'Doe', '2000 Humboldt St., #6', '97213');
    INSERT INTO CUSTOMER VALUES(1009, 'Mr', 'George', 'Howe', '111 B Parkway, #23', '75243');
    INSERT INTO CUSTOMER VALUES(1010, 'Mr', 'Frank', 'Miller', '27 5th St., 76', '95054');
    INSERT INTO CUSTOMER VALUES(1011, 'Mrs', 'Susan', 'Baker', '200 MAIN STREET, #94', '90018');
    INSERT INTO CUSTOMER VALUES(1012, 'Mr', 'Joseph', 'Peters', '700 S. Ash St., APT.12', '92714');
    INSERT INTO CUSTOMER VALUES(1013, 'Company', NULL, 'TOOLware', '410 Mariposa St., #10', '20019');
    INSERT INTO CUSTOMER VALUES(1014, 'Mr', 'Antony', 'Jenkins', '55 A Parkway, #15', '20903');

    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(100, 1000, 11, 'single', '2020-12-24', '2020-12-27');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(110, 1001, 11, 'double', '2020-12-24', '2021-01-03');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(120, 1002, 15, 'suite', '2020-11-14', '2020-11-18');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(130, 1009, 21, 'single', '2019-02-01', '2019-02-03');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(150, 1006, 17, 'double', '2019-03-14', '2019-03-24');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(140, 1013, 20, 'double', '2020-04-12', '2020-04-30');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(160, 1011, 17, 'single', '2020-04-12', '2020-04-15');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(170, 1014, 25, 'suite', '2020-09-01', '2020-09-03');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(180, 1001, 22, 'double', '2020-12-23', '2021-01-08');
    INSERT INTO RESERVATION(rno, cno, hno, type, arrival, departure) VALUES(190, 1013, 24, 'double', '2020-11-14', '2020-11-17');

    INSERT INTO MAINTENANCE VALUES(10, 24, 'Replace pool liner and pump', '2019-03-21', 'Discount Pool Supplies');
    INSERT INTO MAINTENANCE VALUES(11, 25, 'Renovate the bar area.  Replace TV and speakers', '2020-11-29', 'TV and Audio Superstore');
    INSERT INTO MAINTENANCE VALUES(12, 26, 'Roof repair due to storm', null, null);
    COMMIT;
    ```

    Additional details on the SQL used above can be found at [INSERT Statement for Data Lake Relational Engine](https://urldefense.com/v3/__https://help.sap.com/viewer/19b3964099384f178ad08f2d348232a9/latest/en-US/a61fdeff84f21015aa66b9add387d7f9.html__;!!GF_29dbcQIUBPA!3-VGFthfLzox1V6QHvLyMpJH64RtcqU-Eouowl25Y9BFMo6d1FKf_CKiAj8866Ac9_PtxCoS_TAavxoj127uobst$ [help[.]sap[.]com]). Moreover, the [LOAD TABLE Statement for Data Lake Relational Engine](https://urldefense.com/v3/__https://help.sap.com/viewer/19b3964099384f178ad08f2d348232a9/latest/en-US/7ca3f60902f3473296cb309533d89210.html__;!!GF_29dbcQIUBPA!3-VGFthfLzox1V6QHvLyMpJH64RtcqU-Eouowl25Y9BFMo6d1FKf_CKiAj8866Ac9_PtxCoS_TAavxoj16KCGaqD$ [help[.]sap[.]com]) can be used for efficient mass insertion into a database table from a file with ASCII or binary data.

    >Autocommit is set to on in the SQL Console of the database explorer, while in DBISQL it is set to off.  A series of insert statements will run quicker in the SQL Console if they are surrounded with begin and end or if autocommit is set to off.
    >
    ```SQL
    begin
    INSERT INTO HOTEL.ROOM VALUES(11, 'garden view', 13, 190.00);
    INSERT INTO HOTEL.ROOM VALUES(11, 'connecting room', 15, 175.00);
    end;
    ```
    >
    ```SQL
    set temporary option auto_commit= 'off';
    INSERT INTO HOTEL.ROOM VALUES(11, 'triple', 7, 235.00);
    INSERT INTO HOTEL.ROOM VALUES(11, 'quad', 5, 275.00);
    set temporary option auto_commit= 'on';
    ```
    >
    >Autocommit can also be set via the connection settings dialog.
    >
    >![autocommit setting](hxe2_vm_start_0.png)


2. Notice that pressing ctrl-space brings up auto complete (GUI mode only).

    ![auto complete](hxe2_vm_start_0.png)

    Query a table, a view, invoke a function, and call a stored procedure.

    ```SQL
    SET SCHEMA HOTEL;
    SELECT * FROM HOTEL;
    SELECT * FROM HOTEL_ROOMS_VIEW;
    SELECT AVERAGE_PRICE('single'), AVERAGE_PRICE('double'), AVERAGE_PRICE('suite') FROM DUMMY;
    CALL SHOW_RESERVATIONS(11, '2020-12-24');
    ```

    ![Query in DBISQL](dbisql-query.png)

3. DBISQL can also execute SQL from the command line or from a provided file. A few examples are shown below.

    ```Shell
    dbisql -c "uid=USER1;pwd=Password1;host=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.iq.hdl.trial-XXXX.hanacloud.ondemand.com:443;ENC=TLS(tls_type=rsa;direct=yes)" "select * from HOTEL.CUSTOMER;"
    dbisql -c "uid=USER1;pwd=Password1;host=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.iq.hdl.trial-XXXX.hanacloud.ondemand.com:443;ENC=TLS(tls_type=rsa;direct=yes)" sql.sql
    ```

    ![DBISQL in batch mode](dbisql-batch.png)

