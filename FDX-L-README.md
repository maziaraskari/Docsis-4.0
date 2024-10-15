# FDX-L
Configuration CRD Tracking for the FDX-L Project version 2 9/10/24
Instructions:

 
 1. Remove 2nd D3.1 ofdma channel :  "docs-chan-id": 194,

                  {
                    "admin-state": "up",
                    "docs-chan-id": 194,
                    "lower-bdry-freq": 815000000,
                    "lower-guard-band-index": 1,
                    "ofdm-channel-index": 1,
                    "ofdm-profile": [
                      {
                        "ofdm-modulation-default": "qam64",
                        "ofdm-profile-index": 0,
                        "yang-ext": {
                          "ccap-harmonic:hysteresis": "1.0",
                          "ccap-harmonic:threshold": "21.0"
                        }
                      },
                      {
                        "ofdm-modulation-default": "qam256",
                        "ofdm-profile-index": 1,
                        "yang-ext": {
                          "ccap-harmonic:hysteresis": "1.0",
                          "ccap-harmonic:threshold": "27.0"
                        }
                      },
                      {
                        "ofdm-modulation-default": "qam1024",
                        "ofdm-profile-index": 2,
                        "yang-ext": {
                          "ccap-harmonic:hysteresis": "1.0",
                          "ccap-harmonic:threshold": "34.0"
                        }
                      },
                      {
                        "ofdm-modulation-default": "qam2048",
                        "ofdm-profile-index": 3,
                        "yang-ext": {
                          "ccap-harmonic:hysteresis": "1.0",
                          "ccap-harmonic:threshold": "37.0"
                        }
                      },
                      {
                        "ofdm-modulation-default": "qam16",
                        "ofdm-profile-index": 255,
                        "yang-ext": {
                          "ccap-harmonic:hysteresis": "1.0",
                          "ccap-harmonic:threshold": "15.0"
                        }
                      }
                    ],
                    "plc-blk-freq": 990000000,
                    "subcarrier-spacing": "25khz",
                    "upper-bdry-freq": 1007000000,
                    "upper-guard-band-index": 2,
                    "yang-ext": {
                      "ccap-harmonic:default-profile": 0,
                      "ccap-harmonic:query-load": "1.0"
                    }

                  }

 2. Locate the “allocated-spectrum” Update the value from 384 to 288.

 3.   For DUU change the admin state of first fdx-ofdm-channel to "admin-state": "up", (for "fdx-ofdm-channel-index": 0,)
      For UDU change the admin state of second fdx-ofdm-channel to "admin-state": "up", (for "fdx-ofdm-channel-index": 1,)
      For UUD change the admin state of 3rd fdx-ofdm-channel to "admin-state": "up", (for "fdx-ofdm-channel-index": 2,)

      Change the subcarrier spacing to 25KHz.
      and verify "cyclic-prefix": 256, and roll-off period "rolloff-period": 128,
                  
 4. Remove 4th FDX-OFDMA.  "fdx-ofdma-channel-index": 3,

                ,
                {
                  "provisioned-attribute-mask": "bonded",
                  "fdx-ofdma-channel-index": 3,
                  "ccap-harmonic:mod-prof-management": {
                    "control": true,
                    "corrected-fec": 95,
                    "ignored-mslot-pct": 8,
                    "mer-hysteresis": 10,
                    "mer-margin": -20,
                    "mer-poll-interval": 5,
                    "min-codewords": 1000,
                    "uncorrected-fec": 1,
                    "unfit-period-minutes": 10
                  },
                  "ccap-harmonic:initial-ranging-frequency-hz": 439575000,
                  "ccap-harmonic:fine-ranging-frequency-hz": 420000000,
                  "ccap-harmonic:pre-equalization": {
                    "control": true,
                    "probe-timing-adjust": true,
                    "set-interval": 40
                  },
                  "admin-state": "down",
                  "power-adjust": 0,
                  "ofdma-chan-template": 17
                }									

5. Change the admin-state of all 3 fdx-ofdma channels to "down".

6. Remove the "fdx-ofdma-channel-index": 3" from fdx-ofdma-channel-index" parameter.
									,
									{
										"fdx-ofdma-channel-index": 3,
										"fdx-resource-index": 0,
										"slot": 4610
									}


7. Add "subband-id": 2":

									"sub-band-config": [
										{
											"direction": "upstream",
											"subband-id": 0
										},
										{
											"direction": "upstream",
											"subband-id": 1
										},
										{
											"direction": "upstream",
											"subband-id": 2
										}






8. Follow the pattern of each RPD slot number, mac-domain, DSG channels and line card name specific to each RPD.
9. Verify the admin-state of the FDX-OFDM channel is "up" per following :

    For DUU : Change  "fdx-ofdm-channel-index": 0,  Change the "admin-state": "up",  from down 
              
    For UDU : Change  "fdx-ofdm-channel-index": 1,  Change the "admin-state": "up",  from down 

    For UUD : Change  "fdx-ofdm-channel-index": 2,  Change the "admin-state": "up",  from down 



10. Change the direction of sub-bands to "downstream" accordingly:

          "sub-band-config": [
            {
              "direction": "downstream",
              "subband-id": 0
            },
            {
              "direction": "downstream",
              "subband-id": 1
            },
            {
              "direction": "downstream",
              "subband-id": 2
            }
          ],
		

11. Add new Downstream Bonding group 24L:  Pay attention to  "fdx-ofdm-channel-index": 0, and add according to DUU UDU or UUD.

      {
        "bonding-group-name": "Ds83:0/0:D24L",
        "docsis-down-channel-ref": [
          {
            "down-channel": 0,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 1,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 2,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 3,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 4,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 5,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 6,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 7,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 8,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 9,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 10,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 11,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 12,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 13,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 14,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 15,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 16,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 17,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 18,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 19,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 20,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 21,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 22,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 23,
            "ds-rf-port": 0,
            "slot": 21248
          }
        ],
        "downstream-bonding-mac-domain-name": "83:0/0.0",
        "dsid-resequencing-wait-time": 1,
        "dsid-resequencing-warning-threshold": 1,
        "ofdm-channel-ref": [
          {
            "ds-rf-port": 0,
            "ofdm-channel": 0,
            "slot": 21248
          }
        ],
        "yang-ext": {
          "ccap-harmonic:admin-state": "up",
          "ccap-harmonic:fdx-ofdm-ref": [
            {
              "fdx-ofdm-channel-index": 0,  <<<<<<<<<<<<<<<<<. change index accordingly 0 for DUU, 1 for UDU and 2 for UUD
              "fdx-resource-index": 0,
              "slot": 21248
            }
          ]
        }
      },


12.  remove second ofdm channel from downstream bonding group bonding-group-name": "Ds83:0/0:D5",

      {
              "bonding-group-name": "Ds83:0/0:D5",
              "docsis-down-channel-ref": [
                {
                  "down-channel": 0,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 1,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 2,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 3,
                  "ds-rf-port": 0,
                  "slot": 21248
                }
              ],
              "downstream-bonding-mac-domain-name": "83:0/0.0",
              "dsid-resequencing-wait-time": 130,
              "dsid-resequencing-warning-threshold": 130,
              "ofdm-channel-ref": [
                {
                  "ds-rf-port": 0,
                  "ofdm-channel": 0,
                  "slot": 21248
                }
              ],
              "yang-ext": {
                "ccap-harmonic:admin-state": "up"
              }
            },

13.  remove downstream bonding group 10A and 10B
13.  remove 2nd d3.1 ofdm channle from downstream bonding group 10C


14. Add Downstream bonding groups 5L and 6L :
            ,
            {
              "bonding-group-name": "Ds83:0/0:D6L",
              "docsis-down-channel-ref": [
                {
                  "down-channel": 0,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 1,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 2,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 3,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 4,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 5,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 6,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 7,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 8,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 9,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 10,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 11,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 12,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 13,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 14,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 15,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 16,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 17,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 18,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 19,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 20,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 21,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 22,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 23,
                  "ds-rf-port": 0,
                  "slot": 21248
                }
              ],
              "downstream-bonding-mac-domain-name": "83:0/0.0",
              "dsid-resequencing-wait-time": 130,
              "dsid-resequencing-warning-threshold": 130,
              "ofdm-channel-ref": [
                {
                  "ds-rf-port": 0,
                  "ofdm-channel": 0,
                  "slot": 21248
                }
              ],
              "yang-ext": {
                "ccap-harmonic:admin-state": "up",
                "ccap-harmonic:fdx-ofdm-ref": [
                  {
                    "fdx-ofdm-channel-index": 0,            <<<<<<<<<<<<<<<<<. change index accordingly 0 for DUU, 1 for UDU and 2 for UUD
                    "fdx-resource-index": 0,            
                    "slot": 21248
                  }
                ]
              }
            },
            {
              "bonding-group-name": "Ds83:0/0:D5L",
              "docsis-down-channel-ref": [
                {
                  "down-channel": 0,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 1,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 2,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 3,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 4,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 5,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 6,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 7,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 8,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 9,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 10,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 11,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 12,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 13,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 14,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 15,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 16,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 17,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 18,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 19,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 20,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 21,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 22,
                  "ds-rf-port": 0,
                  "slot": 21248
                },
                {
                  "down-channel": 23,
                  "ds-rf-port": 0,
                  "slot": 21248
                }
              ],
              "downstream-bonding-mac-domain-name": "83:0/0.0",
              "dsid-resequencing-wait-time": 130,
              "dsid-resequencing-warning-threshold": 130,
              "ofdm-channel-ref": [
                {
                  "ds-rf-port": 0,
                  "ofdm-channel": 0,
                  "slot": 21248
                }
              ],
              "yang-ext": {
                "ccap-harmonic:admin-state": "up"
              }
            }



15. Change the RBA schedule to downstream to DUU; UDU or UUD accordingly :


            ,
            "ccap-harmonic:fdx-rba-schedule": [
              {
                "fdx-rba-schedule-step": [
                  {
                    "duration-msec": 10000,
                    "fdx-direction-set": "DUU",    <<< this is changed each time fro DUU, UDU, or UUD
                    "step-index": 0
                  }
                ],
                "rba-schedule-name": "rba1"
              }
            ]

16.  remove the second ofdm from ds-ofdm-non-primary-channel-ref: 

"ccap-harmonic:ds-ofdm-non-primary-channel-ref": [
                  {
                    "ds-rf-port": 0,
                    "ofdm-channel": 0,
                    "slot": 21248
                  }



17.  Change to "cyclic-prefix": 256, from "cyclic-prefix": 512, in all 3 "fdx-ofdm-channel" and add to d3.1 OFDM channel.

18.  Change to "rolloff-period": 128, from "rolloff-period": 192, in all 3 "fdx-ofdm-channel" and add to the D3.1 OFDM cahnnel.

D3.1 OFDM:

"ofdm-channel": [

        {

          "admin-state": "up",

          "cyclic-prefix": 256,

         "rolloff-period": 128,
         .
         .
         .]






19.  For DUU Change to 


        "sub-band-config": [
          {
            "direction": "downstream",
            "subband-id": 0
          },
          {
            "direction": "upstream",
            "subband-id": 1
          },
          {
            "direction": "upstream",
            "subband-id": 2
          }
        ],


for UDU and UUD move the downstream channel in above config accordingly.


20.  Add U8L Bonding group for DUU ; for UDU use correct indexes 0 and 2 ; for UUD use indexes 0 and 1

        ,
        {
          "bonding-group-name": "Us83:0/0:U8L",
          "upstream-logical-channel-ref": [
            {
              "slot": 21248,
              "upstream-logical-channel": 0,
              "upstream-physical-channel": 0,
              "us-rf-port": 0
            },
            {
              "slot": 21248,
              "upstream-logical-channel": 0,
              "upstream-physical-channel": 1,
              "us-rf-port": 0
            },
            {
              "slot": 21248,
              "upstream-logical-channel": 0,
              "upstream-physical-channel": 2,
              "us-rf-port": 0
            },
            {
              "slot": 21248,
              "upstream-logical-channel": 0,
              "upstream-physical-channel": 3,
              "us-rf-port": 0
            }
          ],
          "ofdma-channel-ref": [
            {
              "ofdma-channel": 0,
              "slot": 21248,
              "us-rf-port": 0
            }
          ],
          "yang-ext": {
            "ccap-harmonic:admin-state": "up",
            "ccap-harmonic:fdx-ofdma-ref": [
              {
                "fdx-ofdma-channel-index": 1,
                "fdx-resource-index": 0,
                "slot": 21248
              },
              {
                "fdx-ofdma-channel-index": 2,
                "fdx-resource-index": 0,
                "slot": 21248
              }
            ]
          }



21.  Change all these values to following in all bonding groups: 

 "dsid-resequencing-wait-time": 130,

 "dsid-resequencing-warning-threshold": 128,

22.  Add following ds bonding group 10D and change the fdx-ofdm channel index in the bonding group accordingly to UDU (1) or UUD (2)


      ,
      {
        "bonding-group-name": "Ds83:0/0:D10D",
        "docsis-down-channel-ref": [
          {
            "down-channel": 16,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 17,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 18,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 19,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 20,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 21,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 22,
            "ds-rf-port": 0,
            "slot": 21248
          },
          {
            "down-channel": 23,
            "ds-rf-port": 0,
            "slot": 21248
          }
        ],
        "downstream-bonding-mac-domain-name": "83:0/0.0",
        "dsid-resequencing-wait-time": 130,
        "dsid-resequencing-warning-threshold": 128,
        "ofdm-channel-ref": [
          {
            "ds-rf-port": 0,
            "ofdm-channel": 0,
            "slot": 21248
          }
        ],
        "yang-ext": {
          "ccap-harmonic:admin-state": "up",
          "ccap-harmonic:fdx-ofdm-ref": [
            {
              "fdx-ofdm-channel-index": 0,
              "fdx-resource-index": 0,
              "slot": 21248
            }
          ]
        }
      },


23 - Change upper boundry for fdx-ofdm-exclusions from 484 MHz to 483 MHz ; 



