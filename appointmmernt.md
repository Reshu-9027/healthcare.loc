
# changes in  patient model
## Replace this function
``` php
  
    public function getuser_appointments($data)
    {
	if($data['tense']=='past'){ $con="and appointment_date <'".date('Y-m-d')."' "; } else { $con="and appointment_date > '".date('Y-m-d')."' "; }
    if($data['lan']=='en') { 
                $query=$this->db->query("SELECT `appointment_id`, `appointment_date`, `appointment_time`, `dr_image`, `appointment_end`, `doctor_id`, `patient_id`, `user_id`, `patient_type`, `consult_mode`, `created` ,dr_name , dr_clinic_detail as clinic ,dr_clinic_address1 as ads1 ,dr_clinic_address2 as ads2 FROM `doctor_appointments` join dr_details   on doctor_appointments.`doctor_id`=dr_details.`dr_id` join dr_clinic on dr_clinic.dr_id= doctor_appointments.`doctor_id` WHERE `user_id` = '".$data['id']."' $con order by appointment_date DESC ");
       return $query->result();

    } else {

            $query=$this->db->query("SELECT `appointment_id`, `appointment_date`, `appointment_time`, `dr_image`, `appointment_end`, `doctor_id`, `patient_id`, `user_id`, `patient_type`, `consult_mode`, `created` ,dr_name ,ln_dr_clinic_detail as clinic, ln_dr_clinic_address1 as ads1 ,ln_dr_clinic_address2 as ads2 FROM `doctor_appointments` join dr_details   on doctor_appointments.`doctor_id`=dr_details.`dr_id` join ln_dr_clinic ln_dr_clinic.dr_id= doctor_appointments.`doctor_id` WHERE `user_id` = '".$data['id']."' $con order by appointment_date DESC ");
            return $query->result();

     }		

    
    }
```

# Replace this with append data in user_appointments.html

  ``` javascript
     var htmlstr = `<div class="col-sm-6 col-md-3 mb-60 sm-text-center">
                                <div class="team maxwidth400">
                                    <div class="thumb"><img class="mx-auto" src="admin/uploads/media/cache/200x200-`+obj.data[i].dr_image+`" style="max-height: 200px;" alt=""></div>
                                    <div class="content border-1px p-15 bg-white-light">
                                        <h4 class="name mb-0 mt-0">`+obj.data[i].dr_name+`</h4>
                                        <ul class="list-inline font-13 mb-20">
                                            <li><i class="fa fa-calendar mr-5"></i>`+aptime(obj.data[i].appointment_date+` `+obj.data[i].appointment_time )+`</li>
                                            
                                        </ul>
                                        <ul class="list-inline font-13 mb-20">
                                            <li><i class="fa fa-internet-explorer mr-5"></i>Type : `+obj.data[i].consult_mode+`</li>
                                        </ul>`;

                        if(obj.data[i].consult_mode == 'online')
                        {
                            htmlstr += `<a class="btn btn-theme-colored btn-sm mx-auto flip" href="user_online_Consultation.html" target="_blank">Start Consultation</a>`
                        }
                        else
                        {

                            htmlstr +=`<ul class="list-inline font-13 mb-20">
                                            <li><i class="fa fa-heartbeat mr-5"></i><b>`+obj.data[i].clinic +`</b></li>
                                            <li><i class="fa fa-map-marker mr-5"></i>`+obj.data[i].ads1 +"  "+obj.data[i].ads2+`</li></ul>`;
                        }
                                 
                            htmlstr +=`<a class="btn btn-theme-colored btn-sm mx-auto flip" href="doctors_details_en.html" onclick="doc_details(`+obj.data[i].doctor_id+`,0);"  >viewdetails</a>
                            </div>
                                </div>
                            </div>`;       


                        $('#doctor-list-row').append(htmlstr);
                        
                        
                        
    ```
    
## Replace this append data in user_appointments_vn.html

  ``` javacsript

     var htmlstr = `<div class="col-sm-6 col-md-3 mb-60 sm-text-center">
                                <div class="team maxwidth400">
                                    <div class="thumb"><img class="mx-auto" src="admin/uploads/media/cache/200x200-`+obj.data[i].dr_image+`" style="max-height: 200px;" alt=""></div>
                                    <div class="content border-1px p-15 bg-white-light">
                                        <h4 class="name mb-0 mt-0">`+obj.data[i].dr_name+`</h4>
                                        <ul class="list-inline font-13 mb-20">
                                            <li><i class="fa fa-calendar mr-5"></i>`+aptime(obj.data[i].appointment_date+` `+obj.data[i].appointment_time )+`</li>
                                            
                                        </ul>
                                        <ul class="list-inline font-13 mb-20">
                                            <li><i class="fa fa-internet-explorer mr-5"></i>kiểu : `+obj.data[i].consult_mode+`</li>
                                        </ul>`;

                        if(obj.data[i].consult_mode == 'online')
                        {
                            htmlstr += `<a class="btn btn-theme-colored btn-sm mx-auto flip" href="user_online_Consultation.html" target="_blank">bắt đầu tham vấn</a>`
                        }
                        else
                        {

                            htmlstr +=`<ul class="list-inline font-13 mb-20">
                                            <li><i class="fa fa-heartbeat mr-5"></i><b>`+obj.data[i].clinic +`</b></li>
                                            <li><i class="fa fa-map-marker mr-5"></i>`+obj.data[i].ads1 +"  "+obj.data[i].ads2+`</li></ul>`;
                        }
                                 
                            htmlstr +=`  
                                <a class="btn btn-theme-colored btn-sm mx-auto flip" href="doctors_details_vn.html" onclick="doc_details(`+obj.data[i].doctor_id+`,0);"  >xem chi ti?ts</a>
                            </div>
                                </div>
                            </div>`;       


                        $('#doctor-list-row').append(htmlstr);

```



  ## Add this function in user_appointments.html
  ``` javascript
         function doc_details(docId) {
            localStorage.setItem('docid', docId);
            window.location.replace('doctors_details_en.html');
        }
  ```
  
  ## Add this function in user_appointments_vn.html
   ``` javascript
         function doc_details(docId) {
            localStorage.setItem('docid', docId);
            window.location.replace('doctors_details_vn.html');
        }
  ```



