<!DOCTYPE html>
<html lang="en" ng-app="assessmentApp">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assessment Form</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: auto;
            padding: 20px;
            background-color: white;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        label {
            font-weight: bold;
        }
        input, select, textarea {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .form-section {
            margin-bottom: 20px;
        }
        .assessment-questions input {
            width: 80%;
            margin: 5px 0;
        }
        .signature {
            margin-top: 30px;
            text-align: center;
        }
    </style>
</head>
<body ng-controller="AssessmentController">

    <div class="container">
        <h1>Candidate Assessment Form</h1>
        
        <!-- Personal Information -->
        <div class="form-section">
            <label>Candidate Name:</label>
            <input type="text" ng-model="candidateName" placeholder="Enter candidate name" />
        </div>

        <div class="form-section">
            <label>Date of Birth:</label>
            <input type="date" ng-model="dob" />
        </div>

        <div class="form-section">
            <label>Gender:</label>
            <select ng-model="gender">
                <option value="Male">Male</option>
                <option value="Female">Female</option>
                <option value="Other">Other</option>
            </select>
        </div>

        <div class="form-section">
            <label>Email:</label>
            <input type="email" ng-model="email" placeholder="Enter email" />
        </div>

        <div class="form-section">
            <label>Phone Number:</label>
            <input type="tel" ng-model="phone" placeholder="Enter phone number" />
        </div>

        <!-- Qualifications -->
        <div class="form-section">
            <label>School +2 - Subject and GPA:</label>
            <input type="text" ng-model="schoolSubject" placeholder="Subject" />
            <input type="number" ng-model="schoolGPA" placeholder="GPA" />
        </div>

        <div class="form-section">
            <label>Bachelor's Degree - Subject and GPA:</label>
            <input type="text" ng-model="bachelorSubject" placeholder="Subject" />
            <input type="number" ng-model="bachelorGPA" placeholder="GPA" />
        </div>

        <div class="form-section">
            <label>Do you have a Degree?</label>
            <select ng-model="degree">
                <option value="Yes">Yes</option>
                <option value="No">No</option>
            </select>
            <div ng-if="degree === 'Yes'">
                <label>Degree Points:</label>
                <input type="number" ng-model="degreePoints" placeholder="Enter degree points" />
            </div>
        </div>

        <!-- Evaluation Criteria -->
        <h3>Evaluation Criteria</h3>
        <div class="form-section" ng-repeat="(criterion, score) in evaluationCriteria">
            <label>{{ criterion }}:</label>
            <input type="number" ng-model="evaluationCriteria[criterion]" min="0" max="10" />
        </div>

        <!-- Assessment Questions -->
        <h3>Assessment Questions</h3>
        <div class="assessment-questions">
            <div ng-repeat="i in [1,2,3,4,5]">
                <label>Question {{i}}:</label>
                <textarea ng-model="questions[i]" placeholder="Enter your answer"></textarea>
            </div>
        </div>

        <!-- Other Details -->
        <div class="form-section">
            <label>Position Applied:</label>
            <input type="text" ng-model="position" placeholder="Enter position applied" />
        </div>

        <div class="form-section">
            <label>Date of Assessment:</label>
            <input type="date" ng-model="assessmentDate" />
        </div>

        <div class="form-section">
            <label>Expected Salary:</label>
            <input type="number" ng-model="expectedSalary" placeholder="Enter expected salary" />
        </div>

        <div class="form-section">
            <label>How many years do you want to work here?</label>
            <input type="number" ng-model="workYears" placeholder="Enter number of years" />
        </div>

        <!-- Signature -->
        <div class="signature">
            <label>Signature:</label>
            <input type="text" ng-model="signature" placeholder="Enter your signature" />
        </div>

        <!-- Submit Button -->
        <button ng-click="generateAssessment()">Generate Assessment</button>

        <!-- Generated Assessment -->
        <h3>Generated Assessment:</h3>
        <pre>{{ assessment }}</pre>
    </div>

    <script>
        angular.module('assessmentApp', [])
            .controller('AssessmentController', function($scope) {
                $scope.candidateName = '';
                $scope.dob = '';
                $scope.gender = '';
                $scope.email = '';
                $scope.phone = '';
                $scope.schoolSubject = '';
                $scope.schoolGPA = '';
                $scope.bachelorSubject = '';
                $scope.bachelorGPA = '';
                $scope.degree = 'No';
                $scope.degreePoints = '';
                $scope.evaluationCriteria = {
                    "Technical Skills": 0,
                    "Problem Solving": 0,
                    "Communication": 0,
                    "Teamwork": 0
                };
                $scope.questions = {};
                $scope.position = '';
                $scope.assessmentDate = '';
                $scope.expectedSalary = '';
                $scope.workYears = '';
                $scope.signature = '';
                $scope.assessment = '';

                $scope.generateAssessment = function() {
                    let assessmentTemplate = `
Assessment Form
----------------
Candidate Name: ${$scope.candidateName}
Date of Birth: ${$scope.dob}
Gender: ${$scope.gender}
Email: ${$scope.email}
Phone: ${$scope.phone}

Qualifications:
----------------
School +2 - Subject: ${$scope.schoolSubject}, GPA: ${$scope.schoolGPA}
Bachelor's Degree - Subject: ${$scope.bachelorSubject}, GPA: ${$scope.bachelorGPA}
Degree: ${$scope.degree} ${($scope.degree === 'Yes' ? 'Points: ' + $scope.degreePoints : '')}

Evaluation Criteria:
---------------------
`;

                    for (let criterion in $scope.evaluationCriteria) {
                        assessmentTemplate += `${criterion}: ${$scope.evaluationCriteria[criterion]}/10\n`;
                    }

                    assessmentTemplate += `
Assessment Questions:
---------------------
`;

                    for (let i = 1; i <= 5; i++) {
                        assessmentTemplate += `Question ${i}: ${$scope.questions[i]}\n`;
                    }

                    assessmentTemplate += `
Position Applied: ${$scope.position}
Date of Assessment: ${$scope.assessmentDate}
Expected Salary: ${$scope.expectedSalary}
Work Years: ${$scope.workYears}

Signature: ${$scope.signature}
`;

                    $scope.assessment = assessmentTemplate;
                };
            });
    </script>
</body>
</html>

