```c
cell ("sky130_fd_sc_hd__and2_1") {
        leakage_power () {
            value : 0.0031719000;                        // Leakage power values for different input conditions (when)
            when : "!A&B";                               // Used by EDA tools for power estimation and optimization
        }
        leakage_power () {
            value : 0.0028440000;
            when : "!A&!B";
        }
        leakage_power () {
            value : 0.0014741000;
            when : "A&B";
        }
        leakage_power () {
            value : 0.0031700000;
            when : "A&!B";
        }
        area : 6.2560000000;                             // Cell area in square microns
        cell_footprint : "sky130_fd_sc_hd__and2";        // Logical cell footprint name for grouping similar cells
        cell_leakage_power : 0.0026650080;               // Total leakage power of the cell (in microwatts)
        driver_waveform_fall : "ramp";                   // Defines the shape of the output falling transition
        driver_waveform_rise : "ramp";                   // Defines the shape of the output rising transition
        pg_pin ("VGND") {
            pg_type : "primary_ground";                  // Specifies that this pin is the primary ground pin
            related_bias_pin : "VPB";                    // Indicates the body-bias pin associated with this ground pin
            voltage_name : "VGND";                       // The name of the voltage rail this pin is connected to
        }
        pg_pin ("VNB") {
            pg_type : "nwell";                           // Indicates this pin is connected to the n-well region
            physical_connection : "device_layer";        // Specifies that the connection is to the device layer (not routing metal)
            voltage_name : "VNB";                        // Name of the associated voltage rail for this pin
        }
        pg_pin ("VPB") {
            pg_type : "pwell";                           // Indicates this pin is connected to the p-well region
            physical_connection : "device_layer";        // Specifies that the connection is to the device layer (not routing metal)
            voltage_name : "VPB";                        // Name of the associated voltage rail for this pin
        }
        pg_pin ("VPWR") {
            pg_type : "primary_power";                   // Indicates this pin provides the main power supply to the cell
            related_bias_pin : "VNB";                    // Specifies that VNB is the bias pin related to this power pin
            voltage_name : "VPWR";                       // Logical name of the voltage rail connected to this power pin
        }
        pin ("A") {
            capacitance : 0.0014620000;                  // Total input pin capacitance
            clock : "false";                             // Whether this pin is a clock input (false = no)
            direction : "input";                         // Signal direction of the pin
            fall_capacitance : 0.0014310000;             // Capacitance for a falling input signal
            internal_power () {
                fall_power ("power_inputs_1") {          // Input transition times for fall power lookup & Corresponding fall power values
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    values("0.0025379000, 0.0025400000, 0.0025448000, 0.0025448000, 0.0025447000, 0.0025445000, 0.0025440000");
                }
                rise_power ("power_inputs_1") {          // Input transition times for rise power lookup & Corresponding rise power values
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    values("-0.001956100, -0.001957000, -0.001959300, -0.001955200, -0.001945900, -0.001924400, -0.001874800");
                }
            }
            max_transition : 1.5000000000;               // Max allowed input signal transition time
            related_ground_pin : "VGND";                 // Pin name for ground reference
            related_power_pin : "VPWR";                  // Pin name for power reference
            rise_capacitance : 0.0014920000;             // Capacitance for a rising input signal
        }
        pin ("B") {
            capacitance : 0.0014960000;
            clock : "false";
            direction : "input";
            fall_capacitance : 0.0014310000;
            internal_power () {
                fall_power ("power_inputs_1") {
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    values("0.0022875000, 0.0022876000, 0.0022879000, 0.0022886000, 0.0022901000, 0.0022938000, 0.0023021000");
                }
                rise_power ("power_inputs_1") {
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    values("-0.002284200, -0.002283900, -0.002283100, -0.002283200, -0.002283500, -0.002284000, -0.002285200");
                }
            }
            max_transition : 1.5000000000;
            related_ground_pin : "VGND";
            related_power_pin : "VPWR";
            rise_capacitance : 0.0015600000;
        }
        pin ("X") {
            direction : "output";                        // Defines the direction of the pin, in this case, it's an output pin.
            function : "(A&B)";                          // Specifies the logical function or expression associated with the pin, in this case, a logical AND between A and B.
            internal_power () {                          // Represents the internal power consumption of the pin
                fall_power ("power_outputs_1") {         // Specifies the fall (or output) power consumption during a high-to-low voltage transition
                    index_1("0.0100000000, 0.0230505800, 0.0531329300, 0.1224745000, 0.2823108000, 0.6507428000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054670, 0.0034084860, 0.0088993300, 0.0232355600, 0.0606665000, 0.1583962000");
                    values("0.0085240000, 0.0074664000, 0.0046369000, -0.003676900, -0.026596400, -0.087127000, -0.245422400", \
                        "0.0083931000, 0.0073403000, 0.0045021000, -0.003805000, -0.026716700, -0.087233700, -0.245554800", \
                        "0.0082197000, 0.0071245000, 0.0042612000, -0.004033200, -0.026937400, -0.087455000, -0.245748300", \
                        "0.0079991000, 0.0069151000, 0.0040167000, -0.004303500, -0.027186600, -0.087673800, -0.245952000", \
                        "0.0080176000, 0.0068765000, 0.0039774000, -0.004402800, -0.027255800, -0.087711400, -0.245954800", \
                        "0.0088907000, 0.0075031000, 0.0041860000, -0.004514700, -0.027130700, -0.087510900, -0.245699200", \
                        "0.0097210000, 0.0083623000, 0.0048614000, -0.003959300, -0.026952200, -0.087195000, -0.245292000");
                }
                related_pin : "A";                       // Specifies the input pin used to characterize the power consumption of this output pin.
                rise_power ("power_outputs_1") {         // Specifies the rise (or output) power consumption during a low-to-high voltage transition
                    index_1("0.0100000000, 0.0230505800, 0.0531329300, 0.1224745000, 0.2823108000, 0.6507428000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054670, 0.0034084860, 0.0088993300, 0.0232355600, 0.0606665000, 0.1583962000");
                    values("0.0094704000, 0.0108522000, 0.0143551000, 0.0232112000, 0.0462251000, 0.1062811000, 0.2614212000", \
                        "0.0093983000, 0.0107825000, 0.0142948000, 0.0232034000, 0.0462224000, 0.1062042000, 0.2627313000", \
                        "0.0092865000, 0.0106624000, 0.0141663000, 0.0231015000, 0.0461635000, 0.1061495000, 0.2630470000", \
                        "0.0091534000, 0.0105032000, 0.0139926000, 0.0228474000, 0.0459524000, 0.1059391000, 0.2624917000", \
                        "0.0090617000, 0.0104091000, 0.0138378000, 0.0227020000, 0.0458110000, 0.1059986000, 0.2611088000", \
                        "0.0093870000, 0.0107110000, 0.0141771000, 0.0227496000, 0.0458959000, 0.1060684000, 0.2626684000", \
                        "0.0102133000, 0.0114561000, 0.0148248000, 0.0237647000, 0.0465589000, 0.1068110000, 0.2629192000");
                }
            }
            internal_power () {
                fall_power ("power_outputs_1") {
                    index_1("0.0100000000, 0.0230505800, 0.0531329300, 0.1224745000, 0.2823108000, 0.6507428000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054670, 0.0034084860, 0.0088993300, 0.0232355600, 0.0606665000, 0.1583962000");
                    values("0.0101951000, 0.0090964000, 0.0061835000, -0.002195800, -0.025150600, -0.085714800, -0.243986000", \
                        "0.0100591000, 0.0089721000, 0.0060136000, -0.002323200, -0.025284600, -0.085834800, -0.244153700", \
                        "0.0099392000, 0.0088303000, 0.0058713000, -0.002460900, -0.025428100, -0.085962400, -0.244240000", \
                        "0.0097425000, 0.0086176000, 0.0056732000, -0.002675700, -0.025604700, -0.086115800, -0.244393500", \
                        "0.0096279000, 0.0084970000, 0.0055326000, -0.002829200, -0.025731000, -0.086200000, -0.244446800", \
                        "0.0101414000, 0.0088554000, 0.0057637000, -0.002614100, -0.025418700, -0.085861200, -0.244071200", \
                        "0.0115284000, 0.0101688000, 0.0071464000, -0.002204000, -0.025332000, -0.085656700, -0.243846800");
                }
                related_pin : "B";
                rise_power ("power_outputs_1") {
                    index_1("0.0100000000, 0.0230505800, 0.0531329300, 0.1224745000, 0.2823108000, 0.6507428000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054670, 0.0034084860, 0.0088993300, 0.0232355600, 0.0606665000, 0.1583962000");
                    values("0.0099540000, 0.0113288000, 0.0148601000, 0.0237230000, 0.0466245000, 0.1064193000, 0.2628997000", \
                        "0.0099071000, 0.0112947000, 0.0147963000, 0.0235943000, 0.0465181000, 0.1070239000, 0.2636375000", \
                        "0.0097941000, 0.0111693000, 0.0146685000, 0.0235634000, 0.0465247000, 0.1069565000, 0.2629234000", \
                        "0.0096171000, 0.0109888000, 0.0144687000, 0.0233895000, 0.0463804000, 0.1063675000, 0.2643670000", \
                        "0.0095336000, 0.0108720000, 0.0143180000, 0.0231603000, 0.0462240000, 0.1062808000, 0.2632289000", \
                        "0.0097039000, 0.0110450000, 0.0144742000, 0.0232250000, 0.0463406000, 0.1059751000, 0.2629322000", \
                        "0.0100696000, 0.0112933000, 0.0147459000, 0.0236581000, 0.0468086000, 0.1071174000, 0.2634866000");
                }
            }
            max_capacitance : 0.1583960000;              // Maximum load capacitance allowed on this pin
            max_transition : 1.5104930000;               // Maximum transition time allowed at this output
            power_down_function : "(!VPWR + VGND)";      // Defines when the pin is powered down
            related_ground_pin : "VGND";                 // Ground net related to this pin
            related_power_pin : "VPWR";                  // Power net related to this pin
            timing () {                                  // Timing arc related to input A → output X
                cell_fall ("del_1_7_7") {                // Output delay values when input transitions from HIGH to LOW
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.1031383000, 0.1090369000, 0.1213519000, 0.1458819000, 0.1983965000, 0.3245319000, 0.6507022000", \
                        "0.1078665000, 0.1139983000, 0.1263610000, 0.1508638000, 0.2034434000, 0.3294200000, 0.6551888000", \
                        "0.1206382000, 0.1264383000, 0.1387166000, 0.1632862000, 0.2158505000, 0.3420344000, 0.6674351000", \
                        "0.1518939000, 0.1576136000, 0.1699008000, 0.1946328000, 0.2471551000, 0.3730970000, 0.6997410000", \
                        "0.2217431000, 0.2278479000, 0.2405078000, 0.2657816000, 0.3188938000, 0.4447553000, 0.7715348000", \
                        "0.3381809000, 0.3460206000, 0.3619098000, 0.3912823000, 0.4477396000, 0.5756008000, 0.8998989000", \
                        "0.5209776000, 0.5311577000, 0.5518847000, 0.5890423000, 0.6537268000, 0.7846471000, 1.1087463000");
                }
                cell_rise ("del_1_7_7") {                // Output delay values when input transitions from LOW to HIGH
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.0794242000, 0.0864667000, 0.1026603000, 0.1403230000, 0.2350631000, 0.4803423000, 1.1196789000", \
                        "0.0835845000, 0.0906672000, 0.1068781000, 0.1445428000, 0.2394144000, 0.4849028000, 1.1245087000", \
                        "0.0941941000, 0.1012077000, 0.1174051000, 0.1552419000, 0.2499132000, 0.4948990000, 1.1391017000", \
                        "0.1176439000, 0.1247226000, 0.1408894000, 0.1787277000, 0.2738498000, 0.5216426000, 1.1591080000", \
                        "0.1531869000, 0.1607167000, 0.1775795000, 0.2162935000, 0.3111585000, 0.5577310000, 1.1975008000", \
                        "0.1957092000, 0.2050777000, 0.2236305000, 0.2628502000, 0.3577440000, 0.6035356000, 1.2459085000", \
                        "0.2281206000, 0.2408570000, 0.2647271000, 0.3094159000, 0.4035527000, 0.6494337000, 1.2897596000");
                }
                fall_transition ("del_1_7_7") {          // Slope (slew) of output signal when it transitions from HIGH to LOW
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.0234153000, 0.0276024000, 0.0374098000, 0.0604597000, 0.1196515000, 0.2827106000, 0.7157019000", \
                        "0.0233323000, 0.0278020000, 0.0374386000, 0.0605734000, 0.1193361000, 0.2823191000, 0.7152689000", \
                        "0.0236597000, 0.0276025000, 0.0373997000, 0.0604277000, 0.1196194000, 0.2826888000, 0.7158011000", \
                        "0.0234196000, 0.0278806000, 0.0376073000, 0.0605204000, 0.1195282000, 0.2822352000, 0.7153240000", \
                        "0.0272264000, 0.0310681000, 0.0402238000, 0.0623276000, 0.1203398000, 0.2819205000, 0.7129985000", \
                        "0.0383181000, 0.0427394000, 0.0521954000, 0.0735420000, 0.1279992000, 0.2841739000, 0.7151715000", \
                        "0.0565871000, 0.0622415000, 0.0731304000, 0.0952605000, 0.1458810000, 0.2922328000, 0.7139613000");
                }
                related_pin : "A";
                rise_transition ("del_1_7_7") {          // Slope (slew) of output signal when it transitions from LOW to HIGH
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.0273098000, 0.0343713000, 0.0528321000, 0.1021536000, 0.2350815000, 0.5873246000, 1.4968455000", \
                        "0.0273840000, 0.0345314000, 0.0528703000, 0.1020276000, 0.2352878000, 0.5844607000, 1.5043444000", \
                        "0.0272861000, 0.0344569000, 0.0528450000, 0.1020791000, 0.2354850000, 0.5860426000, 1.5063638000", \
                        "0.0281736000, 0.0351018000, 0.0533746000, 0.1020422000, 0.2353452000, 0.5880494000, 1.4962932000", \
                        "0.0322034000, 0.0387938000, 0.0565736000, 0.1041765000, 0.2354808000, 0.5855712000, 1.5004152000", \
                        "0.0416308000, 0.0483148000, 0.0637518000, 0.1082114000, 0.2369543000, 0.5852857000, 1.5016702000", \
                        "0.0592551000, 0.0662234000, 0.0807632000, 0.1200596000, 0.2402845000, 0.5869897000, 1.4960598000");
                }
                timing_sense : "positive_unate";         // Indicates how the output timing is affected by the input transition
                timing_type : "combinational";           // Describes the role of this arc in the cell's operation
            }
            timing () {
                cell_fall ("del_1_7_7") {
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.1209156000, 0.1267669000, 0.1392474000, 0.1641813000, 0.2170752000, 0.3433146000, 0.6697209000", \
                        "0.1256830000, 0.1315514000, 0.1440896000, 0.1689204000, 0.2217300000, 0.3480779000, 0.6741255000", \
                        "0.1389034000, 0.1447728000, 0.1571298000, 0.1822106000, 0.2351275000, 0.3612713000, 0.6883352000", \
                        "0.1707242000, 0.1765896000, 0.1891511000, 0.2141875000, 0.2671949000, 0.3935670000, 0.7206127000", \
                        "0.2458760000, 0.2518757000, 0.2643657000, 0.2895802000, 0.3426674000, 0.4691481000, 0.7961913000", \
                        "0.3811535000, 0.3887241000, 0.4037608000, 0.4324255000, 0.4886735000, 0.6161632000, 0.9428820000", \
                        "0.5985440000, 0.6084658000, 0.6283749000, 0.6649080000, 0.7281128000, 0.8587321000, 1.1855078000");
                }
                cell_rise ("del_1_7_7") {
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.0850944000, 0.0921667000, 0.1083601000, 0.1458898000, 0.2402782000, 0.4848659000, 1.1236686000", \
                        "0.0895209000, 0.0965853000, 0.1127460000, 0.1502857000, 0.2446479000, 0.4893743000, 1.1342737000", \
                        "0.0986120000, 0.1056416000, 0.1217442000, 0.1594235000, 0.2536776000, 0.4999385000, 1.1385588000", \
                        "0.1181221000, 0.1252344000, 0.1413930000, 0.1790957000, 0.2739872000, 0.5188981000, 1.1647858000", \
                        "0.1507703000, 0.1583374000, 0.1753158000, 0.2136513000, 0.3088211000, 0.5540685000, 1.1962887000", \
                        "0.1919068000, 0.2007971000, 0.2194776000, 0.2593621000, 0.3543002000, 0.6003611000, 1.2398564000", \
                        "0.2215551000, 0.2331939000, 0.2570880000, 0.3014003000, 0.3978440000, 0.6441577000, 1.2831414000");
                }
                fall_transition ("del_1_7_7") {
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.0247853000, 0.0292438000, 0.0387901000, 0.0620392000, 0.1209422000, 0.2836178000, 0.7178857000", \
                        "0.0248114000, 0.0293590000, 0.0386992000, 0.0620453000, 0.1208171000, 0.2830563000, 0.7159824000", \
                        "0.0251101000, 0.0293904000, 0.0389104000, 0.0620770000, 0.1207057000, 0.2830010000, 0.7188303000", \
                        "0.0248417000, 0.0293683000, 0.0387121000, 0.0619855000, 0.1210290000, 0.2832596000, 0.7174237000", \
                        "0.0263278000, 0.0301791000, 0.0395620000, 0.0626238000, 0.1210035000, 0.2826644000, 0.7209016000", \
                        "0.0372131000, 0.0416577000, 0.0506625000, 0.0722733000, 0.1267676000, 0.2838049000, 0.7191795000", \
                        "0.0552276000, 0.0607121000, 0.0714424000, 0.0921616000, 0.1430103000, 0.2911559000, 0.7147608000");
                }
                related_pin : "B";
                rise_transition ("del_1_7_7") {
                    index_1("0.0100000000, 0.0230506000, 0.0531329000, 0.1224740000, 0.2823110000, 0.6507430000, 1.5000000000");
                    index_2("0.0005000000, 0.0013054700, 0.0034084900, 0.0088993300, 0.0232356000, 0.0606665000, 0.1583960000");
                    values("0.0273552000, 0.0344671000, 0.0528882000, 0.1019307000, 0.2352126000, 0.5862400000, 1.5035762000", \
                        "0.0273356000, 0.0344320000, 0.0528311000, 0.1021694000, 0.2347287000, 0.5867600000, 1.5065106000", \
                        "0.0274144000, 0.0344779000, 0.0527378000, 0.1020965000, 0.2352505000, 0.5875913000, 1.5000867000", \
                        "0.0280319000, 0.0350671000, 0.0532333000, 0.1021433000, 0.2352442000, 0.5851101000, 1.5104931000", \
                        "0.0312514000, 0.0380700000, 0.0560639000, 0.1036146000, 0.2350764000, 0.5868111000, 1.5016937000", \
                        "0.0386276000, 0.0457767000, 0.0620114000, 0.1072882000, 0.2371053000, 0.5845895000, 1.5012384000", \
                        "0.0545211000, 0.0615401000, 0.0773975000, 0.1178962000, 0.2399373000, 0.5878344000, 1.4954710000");
                }
                timing_sense : "positive_unate";
                timing_type : "combinational";
            }
        }
    }
