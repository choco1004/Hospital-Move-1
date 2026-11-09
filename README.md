# Hospital-Move-1
Hospital Move 1

YOUTUBE : https://www.youtube.com/watch?v=fFsPEoLX8NQ
MATLAB : 

%% 5. Robot Motion Animation

figure('Color','w');

imagesc([1 W], [1 H], map);
set(gca,'YDir','normal');

hold on;
axis equal;
xlim([0 W]);
ylim([0 H]);

grid on;
xlabel('X Position');
ylabel('Y Position');

title('Hospital Robot - A* Navigation Simulation');

colormap([1 1 1; 0.2 0.2 0.2]);

% Start and Goal
plot(start(1), start(2), 'go', ...
    'MarkerSize', 12, 'MarkerFaceColor', 'g');

plot(goal(1), goal(2), 'rp', ...
    'MarkerSize', 15, 'MarkerFaceColor', 'r');

% Planned Path
plot(path(:,1), path(:,2), ...
    'b--', 'LineWidth', 1.5);

% Robot initial position
robot = plot(path(1,1), path(1,2), ...
    'mo', 'MarkerSize', 12, ...
    'MarkerFaceColor', 'm');

% Actual movement trail
trail = animatedline('Color','c', ...
    'LineWidth', 2.5);

legend('Start','Goal','Planned Path', ...
    'Robot','Movement Trail');

% Initial display
drawnow;

% Animation speed
dt = 0.05;

% Start simulation timer
tic;

% Robot movement
for i = 1:size(path,1)

    % Current robot position
    rx = path(i,1);
    ry = path(i,2);

    % Collision verification
    if map(ry,rx) == 1
        error('Robot collision detected!');
    end

    % Update robot position
    set(robot,'XData',rx,'YData',ry);

    % Draw actual movement trail
    addpoints(trail,rx,ry);

    % Refresh animation
    drawnow limitrate;

    pause(dt);

end

% Simulation time
simulationTime = toc;

% Final result
fprintf('\n--- Robot Simulation Results ---\n');

fprintf('Simulation completed successfully!\n');
fprintf('Total path distance: %.2f grid units\n', totalCost);
fprintf('Number of movement points: %d\n', size(path,1));
fprintf('Simulation execution time: %.2f seconds\n', ...
    simulationTime);

title('Hospital Robot - Destination Reached');

hold off;
