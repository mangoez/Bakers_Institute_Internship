# Bakers_Institute_Internship
Shanna and I's project for bakers institute to create a GUI for their heart model
classdef apptest1 < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure                      matlab.ui.Figure
        AVMaxOpeningAreacm2EditFieldLabel  matlab.ui.control.Label
        AVMaxOpeningAreacm2EditField  matlab.ui.control.NumericEditField
        ApplyButton                   matlab.ui.control.Button
    end

    % Callbacks that handle component events
    methods (Access = private)

        % Button pushed function: ApplyButton
        function ApplyButtonPushed(app, event)
            set_param('Michaels_CVModel_0408_fast4/Left Heart/AV_MV_IL/Aortic Valve',...
               'area_max', app.AVMaxOpeningAreacm2EditField.Value)
            simout = sim('Michaels_CVModel_0408_fast4');
        end
    end

    % Component initialization
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure and hide until all components are created
            app.UIFigure = uifigure('Visible', 'off');
            app.UIFigure.Position = [100 100 329 120];
            app.UIFigure.Name = 'MATLAB App';

            % Create AVMaxOpeningAreacm2EditFieldLabel
            app.AVMaxOpeningAreacm2EditFieldLabel = uilabel(app.UIFigure);
            app.AVMaxOpeningAreacm2EditFieldLabel.HorizontalAlignment = 'right';
            app.AVMaxOpeningAreacm2EditFieldLabel.Position = [14 82 163 22];
            app.AVMaxOpeningAreacm2EditFieldLabel.Text = 'AV Max Opening Area (cm^2)';

            % Create AVMaxOpeningAreacm2EditField
            app.AVMaxOpeningAreacm2EditField = uieditfield(app.UIFigure, 'numeric');
            app.AVMaxOpeningAreacm2EditField.Position = [192 82 100 22];
            app.AVMaxOpeningAreacm2EditField.Value = 4;

            % Create ApplyButton
            app.ApplyButton = uibutton(app.UIFigure, 'push');
            app.ApplyButton.ButtonPushedFcn = createCallbackFcn(app, @ApplyButtonPushed, true);
            app.ApplyButton.Position = [192 28 100 22];
            app.ApplyButton.Text = 'Apply';

            % Show the figure after all components are created
            app.UIFigure.Visible = 'on';
        end
    end

    % App creation and deletion
    methods (Access = public)

        % Construct app
        function app = apptest1

            % Create UIFigure and components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
end
