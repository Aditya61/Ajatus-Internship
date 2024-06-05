<script>
    import { onMount } from 'svelte';
    import { parse } from 'csv-parse/browser/esm/sync';
    import Chart from 'chart.js/auto';

    let ageChart = async function(fd) {
        new Chart("ageplot", {
            type: "bar",
            data: {
                labels: Object.keys(fd.age),
                datasets: [{
                    backgroundColor: 'purple',
                    data: Object.values(fd.age)
                }]
            },
            options: {
                responsive: true,
                legend: {display: false},
                title: {
                    display: true,
                    text: "Age"
                }
            }
        });
    } 

    let glucoseChart = async function(fd) {
        new Chart("glucoseplot", {
            type: "bar",
            data: {
                labels: Object.keys(fd.avg_glucose_level),
                datasets: [{
                    backgroundColor: 'green',
                    data: Object.values(fd.avg_glucose_level)
                }]
            },
            options: {
                responsive: true,
                legend: {display: false},
                title: {
                    display: true,
                    text: "Avg. Glucose Level"
                }
            }
        });
    } 

    let bmiChart = async function(fd) {
        new Chart("bmiplot", {
            type: "bar",
            data: {
                responsive: true,
                labels: Object.keys(fd.bmi),
                datasets: [{
                    backgroundColor: 'crimson',
                    data: Object.values(fd.bmi)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "BMI"
                }
            }
        });
    } 

    let workChart = async function(fd) {
        new Chart("workplot", {
            type: "pie",
            data: {
                responsive: true,
                labels: Object.keys(fd.work_type),
                datasets: [{
                    data: Object.values(fd.work_type)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Work Type"
                }
            }
        });
    } 

    let smokingChart = async function(fd) {
        new Chart("smokingplot", {
            type: "pie",
            data: {
                responsive: true,
                labels: Object.keys(fd.smoking_status),
                datasets: [{
                    data: Object.values(fd.smoking_status)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Smoking Status"
                }
            }
        });
    } 

    let genderChart = async function(fd) {
        new Chart("genderplot", {
            type: "pie",
            data: {
                responsive: true,
                labels: Object.keys(fd.gender),
                datasets: [{
                    data: Object.values(fd.gender)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Gender"
                }
            }
        });
    } 

    let hypertensionChart = async function(fd) {
        new Chart("hypertensionplot", {
            type: "pie",
            data: {
                responsive: true,
                labels: Object.keys(fd.hypertension),
                datasets: [{
                    data: Object.values(fd.hypertension)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Hypertension"
                }
            }
        });
    } 

    let heartChart = async function(fd) {
        new Chart("heartplot", {
            type: "pie",
            data: {
                responsive: true,
                labels: Object.keys(fd.heart_disease),
                datasets: [{
                    data: Object.values(fd.heart_disease)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Heart Disease"
                }
            }
        });
    } 

    let marriedChart = async function(fd) {
        new Chart("marriedplot", {
            type: "pie",
            data: {
                responsive: true,
                labels: Object.keys(fd.ever_married),
                datasets: [{
                    data: Object.values(fd.ever_married)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Ever Married"
                }
            }
        });
    } 

    let residenceChart = async function(fd) {
        new Chart("residenceplot", {
            type: "bar",
            data: {
                responsive: true,
                labels: Object.keys(fd.Residence_type),
                datasets: [{
                    backgroundColor: "purple",
                    data: Object.values(fd.Residence_type)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Residence Type"
                }
            }
        });
    } 

    let strokeChart = async function(fd) {
        new Chart("strokeplot", {
            type: "bar",
            data: {
                responsive: true,
                labels: Object.keys(fd.stroke),
                datasets: [{
                    backgroundColor: "cyan",
                    data: Object.values(fd.stroke)
                }]
            },
            options: {
                legend: {display: false},
                title: {
                    display: true,
                    text: "Stroke"
                }
            }
        });
    } 

    let data = [];
    let analyzed_data = {
        no_of_patients:0,
        gender:{},
        age:{},
        hypertension:{},
        heart_disease:{},
        ever_married:{},
        work_type:{},
        Residence_type:{},
        avg_glucose_level:{
            "50:99":0,
            "100:149":0,
            "150:199":0,
            "200:249":0,
            "250:300":0
        },
        bmi:{
            "10:19":0,
            "20:29":0,
            "30:39":0,
            "40:50":0
        },
        smoking_status:{},
        stroke:{}
    };

    onMount(async () => {
        const response = await fetch('/brain_stroke.csv');
        const csvText = await response.text();

        data = parse(csvText, {
            columns: true,
            skip_empty_lines: true
        });
        analyzed_data.no_of_patients=data.length;
        data.forEach(dp => {
            if(analyzed_data.gender[dp.gender]) {
                analyzed_data.gender[dp.gender] += 1
            } else {
                analyzed_data.gender[dp.gender] = 1
            }

            if(analyzed_data.age[dp.age]) {
                analyzed_data.age[dp.age] += 1
            } else {
                analyzed_data.age[dp.age] = 1
            }

            if(analyzed_data.hypertension[dp.hypertension]) {
                analyzed_data.hypertension[dp.hypertension] += 1
            } else {
                analyzed_data.hypertension[dp.hypertension] = 1
            }

            if(analyzed_data.heart_disease[dp.heart_disease]) {
                analyzed_data.heart_disease[dp.heart_disease] += 1
            } else {
                analyzed_data.heart_disease[dp.heart_disease] = 1
            }

            if(analyzed_data.ever_married[dp.ever_married]) {
                analyzed_data.ever_married[dp.ever_married] += 1
            } else {
                analyzed_data.ever_married[dp.ever_married] = 1
            }

            if(analyzed_data.work_type[dp.work_type]) {
                analyzed_data.work_type[dp.work_type] += 1
            } else {
                analyzed_data.work_type[dp.work_type] = 1
            }

            if(analyzed_data.Residence_type[dp.Residence_type]) {
                analyzed_data.Residence_type[dp.Residence_type] += 1
            } else {
                analyzed_data.Residence_type[dp.Residence_type] = 1
            }

            if(dp.avg_glucose_level>=50 && dp.avg_glucose_level<=99){
                analyzed_data.avg_glucose_level['50:99'] += 1
            } else if(dp.avg_glucose_level>=100 && dp.avg_glucose_level<149){
                analyzed_data.avg_glucose_level['100:149'] += 1
            } else if(dp.avg_glucose_level>=150 && dp.avg_glucose_level<=199){
                analyzed_data.avg_glucose_level['150:199'] += 1
            } else if(dp.avg_glucose_level>=200 && dp.avg_glucose_level<=249){
                analyzed_data.avg_glucose_level['200:249'] += 1
            } else if(dp.avg_glucose_level>=250 && dp.avg_glucose_level<=300){
                analyzed_data.avg_glucose_level['250:300'] += 1
            }

            if(dp.bmi>=10 && dp.bmi<=19){
                analyzed_data.bmi['10:19'] += 1
            } else if(dp.bmi>=20 && dp.bmi<=29){
                analyzed_data.bmi['20:29'] += 1
            } else if(dp.bmi>=30 && dp.bmi<=39){
                analyzed_data.bmi['30:39'] += 1
            } else if(dp.bmi>=40 && dp.bmi<=50){
                analyzed_data.bmi['40:50'] += 1
            }

            if(analyzed_data.smoking_status[dp.smoking_status]) {
                analyzed_data.smoking_status[dp.smoking_status] += 1
            } else {
                analyzed_data.smoking_status[dp.smoking_status] = 1
            }

            if(analyzed_data.stroke[dp.stroke]) {
                analyzed_data.stroke[dp.stroke] += 1
            } else {
                analyzed_data.stroke[dp.stroke] = 1
            }
        });
        ageChart(analyzed_data);
        glucoseChart(analyzed_data);
        bmiChart(analyzed_data);
        workChart(analyzed_data);
        smokingChart(analyzed_data);
        genderChart(analyzed_data);
        hypertensionChart(analyzed_data);
        heartChart(analyzed_data);
        marriedChart(analyzed_data);
        residenceChart(analyzed_data);
        strokeChart(analyzed_data);
    });

    function filterdata()
    {
        const gender = document.getElementById('gender').value;
        const age = document.getElementById('age').value;
        const hypertension = document.getElementById('hypertension').value;
        const heartdisease = document.getElementById('heart-disease').value;
        const evermarried = document.getElementById('ever-married').value;
        const worktype = document.getElementById('work-type').value;
        const residencetype = document.getElementById('residence-type').value;
        const agl = document.getElementById('agl').value;
        const bmi = document.getElementById('bmi').value;
        const smokingstatus = document.getElementById('smoking-status').value;
        const stroke = document.getElementById('stroke').value;

        var newdata = data;

        let analyzed_data = {
        no_of_patients:0,
        gender:{},
        age:{},
        hypertension:{},
        heart_disease:{},
        ever_married:{},
        work_type:{},
        Residence_type:{},
        avg_glucose_level:{
            "50:99":0,
            "100:149":0,
            "150:199":0,
            "200:249":0,
            "250:300":0
        },
        bmi:{
            "10:19":0,
            "20:29":0,
            "30:39":0,
            "40:50":0
        },
        smoking_status:{},
        stroke:{}
        };

        
        
        if (gender != "None") {
            newdata = newdata.filter(obj => obj.gender == gender); 
        }
        if (age != "0") {
            newdata = newdata.filter(obj => obj.age == age);
        }
        if (hypertension != "None") {
            newdata = newdata.filter(obj => obj.hypertension == hypertension);
        }
        if (heartdisease != "None") {
            newdata = newdata.filter(obj => obj.heart_disease == heartdisease);
        }
        if (evermarried != "None") {
            newdata = newdata.filter(obj => obj.ever_married == evermarried);
        }
        if (worktype != "None") {
            newdata = newdata.filter(obj => obj.work_type == worktype);
        }
        if (residencetype != "None") {
            newdata = newdata.filter(obj => obj.Residence_type == residencetype);
        }
        if (agl != "None") {
            if (agl == "50-99") {
                newdata = newdata.filter(obj => obj.avg_glucose_level >= 50 && obj.avg_glucose_level <= 99);
            } else if (agl == "100-149") {
                newdata = newdata.filter(obj => obj.avg_glucose_level >= 100 && obj.avg_glucose_level <= 149);
            } else if (agl == "150-199") {
                newdata = newdata.filter(obj => obj.avg_glucose_level >= 150 && obj.avg_glucose_level <= 199);
            } else if (agl == "200-249") {
                newdata = newdata.filter(obj => obj.avg_glucose_level >= 200 && obj.avg_glucose_level <= 249);
            } else if (agl == "250-300") {
                newdata = newdata.filter(obj => obj.avg_glucose_level >= 250 && obj.avg_glucose_level <= 300);
            }
        }
        if (bmi != "None") {
            if (bmi == "10-19") {
                newdata = newdata.filter(obj => obj.bmi >= 10 && obj.bmi <= 19);
            } else if (bmi == "20-29") {
                newdata = newdata.filter(obj => obj.bmi >= 20 && obj.bmi <= 29);
            } else if (bmi == "30-39") {
                newdata = newdata.filter(obj => obj.bmi >= 30 && obj.bmi <= 39);
            } else if (bmi == "40-50") {
                newdata = newdata.filter(obj => obj.bmi >= 40 && obj.bmi <= 50);
            }
        }
        if (smokingstatus != "None") {
            newdata = newdata.filter(obj => obj.smoking_status == smokingstatus);
        }
        if (stroke != "None") {
            newdata = newdata.filter(obj => obj.stroke == stroke);
        }
        
        analyzed_data.no_of_patients=newdata.length;
        newdata.forEach(dp => {
            if(analyzed_data.gender[dp.gender]) {
                analyzed_data.gender[dp.gender] += 1
            } else {
                analyzed_data.gender[dp.gender] = 1
            }

            if(analyzed_data.age[dp.age]) {
                analyzed_data.age[dp.age] += 1
            } else {
                analyzed_data.age[dp.age] = 1
            }

            if(analyzed_data.hypertension[dp.hypertension]) {
                analyzed_data.hypertension[dp.hypertension] += 1
            } else {
                analyzed_data.hypertension[dp.hypertension] = 1
            }

            if(analyzed_data.heart_disease[dp.heart_disease]) {
                analyzed_data.heart_disease[dp.heart_disease] += 1
            } else {
                analyzed_data.heart_disease[dp.heart_disease] = 1
            }

            if(analyzed_data.ever_married[dp.ever_married]) {
                analyzed_data.ever_married[dp.ever_married] += 1
            } else {
                analyzed_data.ever_married[dp.ever_married] = 1
            }

            if(analyzed_data.work_type[dp.work_type]) {
                analyzed_data.work_type[dp.work_type] += 1
            } else {
                analyzed_data.work_type[dp.work_type] = 1
            }

            if(analyzed_data.Residence_type[dp.Residence_type]) {
                analyzed_data.Residence_type[dp.Residence_type] += 1
            } else {
                analyzed_data.Residence_type[dp.Residence_type] = 1
            }

            if(dp.avg_glucose_level>=50 && dp.avg_glucose_level<=99){
                analyzed_data.avg_glucose_level['50:99'] += 1
            } else if(dp.avg_glucose_level>=100 && dp.avg_glucose_level<149){
                analyzed_data.avg_glucose_level['100:149'] += 1
            } else if(dp.avg_glucose_level>=150 && dp.avg_glucose_level<=199){
                analyzed_data.avg_glucose_level['150:199'] += 1
            } else if(dp.avg_glucose_level>=200 && dp.avg_glucose_level<=249){
                analyzed_data.avg_glucose_level['200:249'] += 1
            } else if(dp.avg_glucose_level>=250 && dp.avg_glucose_level<=300){
                analyzed_data.avg_glucose_level['250:300'] += 1
            }

            if(dp.bmi>=10 && dp.bmi<=19){
                analyzed_data.bmi['10:19'] += 1
            } else if(dp.bmi>=20 && dp.bmi<=29){
                analyzed_data.bmi['20:29'] += 1
            } else if(dp.bmi>=30 && dp.bmi<=39){
                analyzed_data.bmi['30:39'] += 1
            } else if(dp.bmi>=40 && dp.bmi<=50){
                analyzed_data.bmi['40:50'] += 1
            }

            if(analyzed_data.smoking_status[dp.smoking_status]) {
                analyzed_data.smoking_status[dp.smoking_status] += 1
            } else {
                analyzed_data.smoking_status[dp.smoking_status] = 1
            }

            if(analyzed_data.stroke[dp.stroke]) {
                analyzed_data.stroke[dp.stroke] += 1
            } else {
                analyzed_data.stroke[dp.stroke] = 1
            }
        });

        const charts = document.getElementById('charts');
        charts.innerHTML = "";
        charts.innerHTML = '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] col-span-2 row-span-2">Age<canvas id="ageplot"></canvas></div> <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] row-span-2">Gender<canvas id="genderplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Avg. Glucose Level<canvas id="glucoseplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Work Type<canvas id="workplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Hypertension<canvas id="hypertensionplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">BMI<canvas id="bmiplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Heart Disease<canvas id="heartplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Smoking Status<canvas id="smokingplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Ever Married<canvas id="marriedplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Residence Type<canvas id="residenceplot"></canvas></div>'+
        '<div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Stroke<canvas id="strokeplot"></canvas></div>'
        

        ageChart(analyzed_data);
        glucoseChart(analyzed_data);
        bmiChart(analyzed_data);
        workChart(analyzed_data);
        smokingChart(analyzed_data);
        genderChart(analyzed_data);
        hypertensionChart(analyzed_data);
        heartChart(analyzed_data);
        marriedChart(analyzed_data);
        residenceChart(analyzed_data);
        strokeChart(analyzed_data);
    }



</script>

<main class="p-5">
    <button on:click={() => { if(document.getElementById('filter').style.display=='block'){document.getElementById('filter').style.display='none'}else{document.getElementById('filter').style.display='block'} }} class="absolute right-5 w-auto flex hover:drop-shadow-md cursor-pointer">
        <p class="text-2xl px-2">Filter</p>
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-8">
        <path stroke-linecap="round" stroke-linejoin="round" d="M10.5 6h9.75M10.5 6a1.5 1.5 0 1 1-3 0m3 0a1.5 1.5 0 1 0-3 0M3.75 6H7.5m3 12h9.75m-9.75 0a1.5 1.5 0 0 1-3 0m3 0a1.5 1.5 0 0 0-3 0m-3.75 0H7.5m9-6h3.75m-3.75 0a1.5 1.5 0 0 1-3 0m3 0a1.5 1.5 0 0 0-3 0m-9.75 0h9.75" />
        </svg>
    </button>
    <div id="filter" class="shadow-black p-5 shadow-sm w-72 h-5/6 absolute right-0 top-36 z-10 bg-white hidden transition-transform">
        <table cellpadding="5">
            <tr>
                <td>Gender</td>
                <td class="w-10"><select id="gender">
                    <option value="None">None</option>
                    <option value="Male">Male</option>
                    <option value="Female">Female</option>
                </select></td>
            </tr>
            <tr>
                <td>Age</td>
                <td><input type="number" value="0" class="border-b-2 w-20 border-black" id="age"></td>
            </tr>
            <tr>
                <td>Hypertension</td>
                <td><select id="hypertension">
                    <option value="None">None</option>
                    <option value="0">False</option>
                    <option value="1">True</option>
                </select></td>
            </tr>
            <tr>
                <td>Heart Disease</td>
                <td><select id="heart-disease">
                    <option value="None">None</option>
                    <option value="0">False</option>
                    <option value="1">True</option>
                </select></td>
            </tr>
            <tr>
                <td>Ever Married</td>
                <td><select id="ever-married">
                    <option value="None">None</option>
                    <option value="Yes">Yes</option>
                    <option value="No">No</option>
                </select></td>
            </tr>
            <tr>
                <td>Work Type</td>
                <td><select id="work-type">
                    <option value="None">None</option>
                    <option value="Private">Private</option>
                    <option value="Self-employed">Self-employed</option>
                    <option value="Govt_job">Govt_job</option>
                    <option value="children">Children</option>
                </select></td>
            </tr>
            <tr>
                <td>Residence Type</td>
                <td><select id="residence-type">
                    <option value="None">None</option>
                    <option value="Urban">Urban</option>
                    <option value="Rural">Rural</option>
                </select></td>
            </tr>
            <tr>
                <td>Avg. Glucose Level</td>
                <td><select id="agl">
                    <option value="None">None</option>
                    <option value="50-99">50-99</option>
                    <option value="100-149">100-149</option>
                    <option value="150-199">150-199</option>
                    <option value="200-249">200-249</option>
                    <option value="250-300">250-300</option>
                </select></td>
            </tr>
            <tr>
                <td>BMI</td>
                <td><select id="bmi">
                    <option value="None">None</option>
                    <option value="10-19">10-19</option>
                    <option value="20-29">20-29</option>
                    <option value="30-39">30-39</option>
                    <option value="40-50">40-50</option>
                </select></td>
            </tr>
            <tr>
                <td>Smoking Status</td>
                <td><select id="smoking-status">
                    <option value="None">None</option>
                    <option value="formerly smoked">Formerly Smoked</option>
                    <option value="never smoked">Never Smoked</option>
                    <option value="smokes">Smokes</option>
                    <option value="Unknown">Unknown</option>
                </select></td>
            </tr>
            <tr>
                <td>Stroke</td>
                <td><select id="stroke">
                    <option value="None">None</option>
                    <option value="0">False</option>
                    <option value="1">True</option>
                </select></td>
            </tr>
        </table>
        <button on:click={filterdata} class="font-semibold bg-blue-400 rounded-sm mt-5 p-3 shadow-sm shadow-black">Apply Filter</button>
    </div>
    
    <div id="charts" class="grid grid-cols-3 grid-flow-row mt-10">
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] col-span-2 row-span-2">Age<canvas id="ageplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] row-span-2">Gender<canvas id="genderplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Avg. Glucose Level<canvas id="glucoseplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Work Type<canvas id="workplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Hypertension<canvas id="hypertensionplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">BMI<canvas id="bmiplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Heart Disease<canvas id="heartplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Smoking Status<canvas id="smokingplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Ever Married<canvas id="marriedplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Residence Type<canvas id="residenceplot"></canvas></div>
        <div class="text-center font-bold drop-shadow-[0px_0px_20px_rgba(0,0,0,0.2)] ">Stroke<canvas id="strokeplot"></canvas></div>
    </div>
      
</main>